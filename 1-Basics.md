# NodeJs-Study-Guide

-Installation:
      
    npm init

-To create a server:

    const http = require('http');

    const server = http.createServer();

    server.listen(4000);
    
-To send a response:

    const server = http.createServer((req, res)=>{

      res.write('Hola');

      res.end();// It is important to end the response

    });
  
  
