- Mongoose

      npm install --save mongoose
      const mongoose = require('mongoose');
      
- Connection to DataBase:
      
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
      
- Schema in mongoose:
      
      const mongoose = require('mongoose');

      const Schema = mongoose.Schema;

      const cardSchema = new Schema({
            front:{ type: String, required: true },
            back:{ type: String, required: true },
            creator:{ type: String, required: true }
      })

      module.exports = mongoose.model('Card', cardSchema);
      
- CRUD mongoose: Read
      
       const getCardById = async(req, res, next)=>{

            const cardId = req.params.cid;

            let card;

            try{
                  card = await CardModel.findById(cardId);
            }catch(error){
                  const errorM = new HttpError('No se pudo', 500);
                  return next(errorM);
            }    

            if(!card){
                  const error = new HttpError('no existe un card con ese id', 404);
                  return next(error);
            }

            res.json({ card: card.toObject( { getters:true } ) });
       }
       
- CRUD mongoose: Read

       const getCardsByUserId = async(req, res, next)=>{
            const userId = req.params.uid;

            let cards;

            try{
                  cards = await CardModel.find({creator:userId});
            }catch(error){
                  const errorM = new HttpError('Algo sucedió', 500);
                  return next(errorM);
            }

            if(!cards || cards.length === 0){
                  const error = new HttpError('no existe un usuario con ese id', 404);
                  return next(error);
            }

            res.json({ cards: cards.map( card => card.toObject({getters:true}) ) });
        }

- CRUD mongoose: Create:

       const createCard = async(req, res, next)=>{
                  const errors = validationResult(req); 
                  if(!errors.isEmpty()){
                  const error = new HttpError('Invalido, revisa la info', 422);
                  throw error;
            }

            const { front, back, creator } = req.body;
            const createdCard = new CardModel({
                  front,
                  back,
                  creator
            })  

            try{
                  await createdCard.save();
            }catch(error){
                  const errorM = new HttpError('No se pudo', 500);
                  return next(errorM);
            }    
            res.status(201).json({card:createdCard});
       }
       
- CRUD mongoose: Update

       const updateCard = async(req, res, next)=>{

            const errors = validationResult(req); 

            if(!errors.isEmpty()){
                  const error = new HttpError('Invalido, revisa la info', 422);
                  throw error;
            }

            const cId = req.params.cid;
            const { front, back } = req.body;

            let card;

            try{
                  card = await CardModel.findById(cId);
            }catch(error){
                  const errorM = new HttpError('No se pudo', 500);
                  return next(errorM);
            }  

            card.front = front;
            card.back = back;

            try{
                  await card.save();

            }catch(error){
                  const errorM = new HttpError('No se pudo actualizar', 500);

                  return next(errorM);
            }

            res.status(200).json({ card:card.toObject({getters:true}) }); 
       }
       
- CRUD mongoose: Delete

       const deleteCard = async(req, res, next)=>{
            const cId = req.params.cid;
            let card;

            try{
                  await CardModel.findByIdAndDelete(cId)

            }catch(error){
                  console.log(error);
            }

            res.json('listo se borró');
       }
