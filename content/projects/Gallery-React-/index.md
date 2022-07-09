---
title: "Gallery Photo"
date: 2022-07-08
draft: false
blog_tags: ["react"]
status: "react"
weight: 26
summary: "We’re going to make a simple Gallery, where we can add photos.
"
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://youtu.be/vUe91uOx7R0"
        weight: 1
    another_link:
        text: "Another github link"
        icon: "fab alt brands fa-github"
        href: "https://github.com/omar-alzant/photo-gallery"
        weight: 2
---


</br>
</br>


## Intro :

We'll create ReactJs code to make the web front-End, and store the photo in Firebase database.

</br>

In this project we use `React` for Front-end, `firebase` for back-end and 
 `framer-motion` package to facilitate creating  the animation ...


</br>

you can view the result  [here](https://ojz-photo-gallery.netlify.app/) .

</br>
</br>

***

## Content :

Our project is divided to some folder in `src` :

1- comps (component):

- ImageGrid.js
- Modal.js
- ProgressBar.js
- Title.js
- UploadForm.js

</br>

2- firebase :

- config.js

</br>

3- hooks :

- useFirestore.js
- useStorage.js

</br>

4- App.js

</br>

5- index.js

</br>

6- index.css


</br>
</br>

***


## Coding :

1- Comps :

- src/comps/ImageGrid.js

Code :

</br>

```javascript

import React from 'react';
import useFirestore from '../hooks/useFirestore';
import { motion } from 'framer-motion';

const ImageGrid = ({ setSelectedImg }) => {
  const { docs } = useFirestore('images');

  return (
    <div className="img-grid">
      {docs && docs.map(doc => (
        <motion.div className="img-wrap" key={doc.id} 
          layout
          whileHover={{ opacity: 1 }}
          onClick={() => setSelectedImg(doc.url)}
        >
          <motion.img src={doc.url} alt="uploaded pic"
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            transition={{ delay: 1 }}
          />
        </motion.div>
      ))}
    </div>
  )
}

export default ImageGrid;

```

</br>

- src/comps/Modal.js


Code : 

</br>

```javascript
import React from 'react';
import { motion } from 'framer-motion';

const Modal = ({ setSelectedImg, selectedImg }) => {

  const handleClick = (e) => {
    if (e.target.classList.contains('backdrop')) {
      setSelectedImg(null);
    }
  }

  return (
    <motion.div className="backdrop" onClick={handleClick}
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
    >
      <motion.img src={selectedImg} alt="enlarged pic" 
        initial={{ y: "-100vh" }}
        animate={{ y: 0 }}
      />
    </motion.div>
  )
}

export default Modal;

```

</br>

- src/comps/ProgressBar.js :

Code :

</br>

```javascript

import React, { useEffect } from 'react';
import useStorage from '../hooks/useStorage';
import { motion } from 'framer-motion';

const ProgressBar = ({ file, setFile }) => {
  const { progress, url } = useStorage(file);

  useEffect(() => {
    if (url) {
      setFile(null);
    }
  }, [url, setFile]);

  return (
    <motion.div className="progress-bar"
      initial={{ width: 0 }}
      animate={{ width: progress + '%' }}
    ></motion.div>
  );
} 

export default ProgressBar;

```

</br>

- src/comps/Title.js

Code :

</br>

```javascript

import React from 'react';

const Title = () => {
  return (
    <div className="title">
      <h1>FireGram</h1>
      <h2>Your Pictures</h2>
      <p>Enjoy with adding your own photo and store it.</p>
    </div>
  )
}

export default Title;

```

</br>

- src/comps/UploadForm.js :

Code :

</br>

```javascript
import React, { useState } from 'react';
import ProgressBar from './ProgressBar';

const UploadForm = () => {
  const [file, setFile] = useState(null);
  const [error, setError] = useState(null);

  const types = ['image/png', 'image/jpeg', 'image/jpg', 'image/gif'];

  const handleChange = (e) => {
    let selected = e.target.files[0];

    if (selected && types.includes(selected.type)) {
      setFile(selected);
      setError('');
    } else {
      setFile(null);
      setError('Please select an image file (png or jpg or jpeg or gif)');
    }
  };

  return (
    <form>
      <label>
        <input type="file" onChange={handleChange} />
        <span>+</span>
      </label>
      <div className="output">
        { error && <div className="error">{ error }</div>}
        { file && <div>{ file.name }</div> }
        { file && <ProgressBar file={file} setFile={setFile} /> }
      </div>
    </form>
  );
}

export default UploadForm;

```

</br>

******

2- Firebase :

- src/firebase/config.js 
</br>

```
We copy the code from the  firebase of this project in the firebase site ):  (firebase -> console -> create app -> code the code from sdk setup and conf ).
```
0
Code :

</br>

```javascript 

import * as firebase from 'firebase/app';
import 'firebase/storage';
import 'firebase/firestore';


// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "Your Api",
  authDomain: "tour Author.firebaseapp.com",
  projectId: "Your Project Id",
  storageBucket: "----.appspot.com",
  messagingSenderId: "----",
  appId: "1:---"
};

// Initialize Firebase
firebase.initializeApp(firebaseConfig);

const projectStorage = firebase.storage();
const projectFirestore = firebase.firestore();
const timestamp = firebase.firestore.FieldValue.serverTimestamp;

export { projectStorage, projectFirestore, timestamp };

```

</br>

*****

3- Hooks :

- src/hooks/useFirestore.js :

Code :

</br>

```javascript

import { useState, useEffect } from 'react';
import { projectFirestore } from '../firebase/config';

const useFirestore = (collection) => {
  const [docs, setDocs] = useState([]);

  useEffect(() => {
    const unsub = projectFirestore.collection(collection)
      .orderBy('createdAt', 'desc')
      .onSnapshot(snap => {
        let documents = [];
        snap.forEach(doc => {
          documents.push({...doc.data(), id: doc.id});
        });
        setDocs(documents);
      });

    return () => unsub();
    // this is a cleanup function that react will run when
    // a component using the hook unmounts
  }, [collection]);

  return { docs };
}

export default useFirestore;

```

</br>

- src/hooks/useStorage.js :

Code :

</br>

```javascript

import { useState, useEffect } from 'react';
import { projectStorage, projectFirestore, timestamp } from '../firebase/config';

const useStorage = (file) => {
  const [progress, setProgress] = useState(0);
  const [error, setError] = useState(null);
  const [url, setUrl] = useState(null);

  useEffect(() => {
    // references
    const storageRef = projectStorage.ref(file.name);
    const collectionRef = projectFirestore.collection('images');
    
    storageRef.put(file).on('state_changed', (snap) => {
      let percentage = (snap.bytesTransferred / snap.totalBytes) * 100;
      setProgress(percentage);
    }, (err) => {
      setError(err);
    }, async () => {
      const url = await storageRef.getDownloadURL();
      const createdAt = timestamp();
      await collectionRef.add({ url, createdAt });
      setUrl(url);
    });
  }, [file]);

  return { progress, url, error };
}

export default useStorage;

```

</br>
</br>

****

4- App.js :

Code :

</br>

```javascript

import React, { useState } from 'react';
import Title from './comps/Title';
import UploadForm from './comps/UploadForm';
import ImageGrid from './comps/ImageGrid';
import Modal from './comps/Modal';

function App() {
  const [selectedImg, setSelectedImg] = useState(null);

  return (
    <div className="App">
      <Title/>
      <UploadForm />
      <ImageGrid setSelectedImg={setSelectedImg} />
      { selectedImg && (
        <Modal selectedImg={selectedImg} setSelectedImg={setSelectedImg} />
      )}
    </div>
  );
}

export default App;

```

</br>
</br>

****

5- index.js :

Code :

</br>

```javascript

import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);


```

</br>
</br>

***

6- index.css :

Code :

</br>

```css

@import url('https://fonts.googleapis.com/css2?family=Noto+Serif:wght@400;700&display=swap');

:root{
  --primary: #efb6b2;
  --secondary: #4e4e4e;
  --error: #ff4a4a;
}

/* base styles & title */
body{
  font-family: "Noto Serif";
  color: var(--secondary);
}
.App{
  max-width: 960px;
  margin: 0 auto;
}
.title h1{
  color: var(--primary);
  font-size: 1.2rem;
  letter-spacing: 2px;
  font-weight: normal;
}
.title h2, .title p{
  text-align: center;
}
.title h2{
  margin-top: 60px;
  font-size: 2.6rem;
}

/* upload form styles */
form{
  margin: 30px auto 10px;
  text-align: center;
}
label input{
  height: 0;
  width: 0;
  opacity: 0;
}
label{
  display: block;
  width: 30px;
  height: 30px;
  border: 1px solid var(--primary);
  border-radius: 50%;
  margin: 10px auto;
  line-height: 30px;
  color: var(--primary);
  font-weight: bold;
  font-size: 24px;
}
label:hover{
  background: var(--primary);
  color: white;
}
.output{
  height: 60px;
  font-size: 0.8rem;
}
.error{
  color: var(--error);
}

/* progress bar styles */
.progress-bar{
  height: 5px;
  background: var(--primary);
  margin-top: 20px;
}

/* image grid styles */
.img-grid{
  margin: 20px auto;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 40px;
}
.img-wrap{
  overflow: hidden;
  height: 0;
  padding: 50% 0;
  /* padding controls height, will always be perfectly square regardless of width */
  position: relative;
  opacity: 0.8;
}
.img-wrap img{
  min-width: 100%;
  min-height: 100%;
  max-width: 130%;
  position: absolute;
  top: 0;
  left: 0;
}

/* modal styles */
.backdrop{
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
}
.backdrop img{
  display: block;
  max-width: 60%;
  max-height: 80%;
  margin: 60px auto;
  box-shadow: 3px 5px 7px rgba(0,0,0,0.5);
  border: 3px solid white;
}


```

</br>
</br>