- Importing the libraries:

      const fs = require('fs');
      const path = require('path');

- Reading a directory:

      const filesPath = path.join(__dirname, 'foldername');
      fs.readdir(filesPath, (error, files)=>{})
