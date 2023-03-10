- Hashing the pasword:
 
       npm install --save bcryptjs

       const bcrypt = require('bcryptjs');
   
       let hashedPassword;

       try{
          hashedPassword = await bcrypt.hash(password, 12);
       }catch(e){
          const error = new HttpError('Error al encriptar el password', 500);
          return next(error);
       }
