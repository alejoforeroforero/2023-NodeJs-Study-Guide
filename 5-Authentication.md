- Installing bcryptjs library:
 
       npm install --save bcryptjs
       
- Hashing the password:

       const bcrypt = require('bcryptjs');
   
       let hashedPassword;

       try{
          hashedPassword = await bcrypt.hash(password, 12);
       }catch(e){
          const error = new HttpError('Error al encriptar el password', 500);
          return next(error);
       }
       
- Comparing the password:

        let isValidPassword = false;

        try{
          isValidPassword = await bcrypt.compare(password, existingUser.password);
        }catch(e){
          const error = new HttpError('Algo pasó al comparar los passwords', 500);
          return next(error);
        }

        if(!isValidPassword){
          const error = new HttpError('credenciales inválidas', 401);
          return next(error);
        }
        
 - Generating the token:

        let isValidPassword = false;

        try{
          isValidPassword = await bcrypt.compare(password, existingUser.password);
        }catch(e){
          const error = new HttpError('Algo pasó al comparar los passwords', 500);
          return next(error);
        }

        if(!isValidPassword){
          const error = new HttpError('credenciales inválidas', 401);
          return next(error);
        }


