- Mongoose

      npm install --save mongoose
      const mongoose = require('mongoose');
      
      **********
      
      mongoose
      .connect(
          'mongodb+srv://<user>:<password>@cluster1.ehnrfax.mongodb.net/xxxx?retryWrites=true&w=majority'
      )
      .then(()=>{
          app.listen(5000);
      })
      .catch(error=>{
          console.log(error);
      });
      
      **********
      
      const mongoose = require('mongoose');

      const Schema = mongoose.Schema;

      const cardSchema = new Schema({
            front:{ type: String, required: true },
            back:{ type: String, required: true },
            creator:{ type: String, required: true }
      })

      module.exports = mongoose.model('Card', cardSchema);
