- Installation:

      npm install --save express body-parser

      npm install --save-dev nodemon

- Package.json -> scripts, nodemon command to restart the server automatically

      "start":"nodemon app.js"
      
- Validator

       npm install --save express-validator
       
- Routes:

       const express = require('express');

       const router = express.Router();

       module.exports = router;
