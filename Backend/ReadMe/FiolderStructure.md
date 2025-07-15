app.js alehda banayi or phir is app ko server.js ka andr import kr ka use kr lyia gya 
is ka alwa server ko he package.json ka nadr main file banayia gyia hain 


### file structure 
1. model folder as obvious it is for schema and the the model and it alsos has hashcode adn the staff related to the authentication encryption etc 

2. routes foder got the routes noiw the interssting thin=ng that we have our her is that our here `note`seconf argument is the `method from the controlle folder` (its logic is written in the controller folder)`note` the first argument is the callback function that is the standard signature defination , why their is a array in the ce4nter and  and how it is linking our here does not get it 


3. controller folder has the actuall logic providing some laye rof authentication checking user name email and pass should be there



4. services folder: prviding services is its work conatins the logic how we are going to create a user in the  data base using th eschema tha is in the data base 


`note`at the end all the thing methods are being used insie the controller folder 

## Summary of hirarchey
```js 
//main flow is this 
app.js → user.routes.js → user.controller.js

```
in the routes we use the middlewares and the controllers of the Controller folder.

inside the controller we use model functions and services function. 
we also have used the model function inside the middleware folder like findone etc    

## Q1 in the routes we passed second paramenter as array which are some test's, why??
basically this second argument is an validator it has relation with the express validator in the routes/user.route.js folder we 
```JS
// route/user.route
const { body } = require('express-validator');
router.post('/register', [
    body('email').isEmail().withMessage('Invalid Email'),
    body('fullname.firstname').isLength({ min: 3 }).withMessage('First name must be at least 3 characters long'),
    body('password').isLength({ min: 6 }).withMessage('Password must be at least 6 characters long')
],
    userController.registerUser
)
//here validator part is 
// [
//     body('email').isEmail().withMessage('Invalid Email'),
//     body('fullname.firstname').isLength({ min: 3 }).withMessage('First name must be at least 3 characters long'),
//     body('password').isLength({ min: 6 }).withMessage('Password must be at least 6 characters long')
// ]

```

the result of these middleware (second argument result) is used inside the inside the controller folder we import it using the:

```JS
// controller/user.controller.js
const { validationResult } = require('express-validator');

module.exports.registerUser = async (req, res, next) => {  

    const errors = validationResult(req); // here is validationResult usage
    if (!errors.isEmpty()) {   
        return res.status(400).json({ errors: errors.array() });
    }
    //code is continue 
```

basically it is doing the basic level validation during the data etery= 0and it is applied over the require fields bcz look at the code of route only firstname is in the array 

## Q how we are importing the routes folder inside the app.js and config them

```js
// code of app.js 
//importing 
const userRoutes = require('./routes/user.routes');
//configuring them 
app.use('/users', userRoutes);

```


## Q With all the routes do we create all the the files in all the above folders 

no, for the Userlogin route we just creaated method insde the User routefile and in the user.controller file other that no extra method like no method of service and model is built

`note` baaar files too create kesi main v nhi krta yani user ka lyia bna rahy too aik dafa sari files ban gyi yani user.route ab is ka andr hum is ka realted routes likh dy ga jais /register /login etc
and same case for controller for the first time we will create the user.controller file and then we will keep on building the controller (yani methods ) as per our needs like regiisterUser for /register route and /loginUser for login route 




## why to write like user.controller.js 
in the user.controller.js  our user is like domain it is for telling that this controller file belongs to the user `note` don't consider it like folder user is not a folder 

chechk how midle ware were intergrated with routes diff with controller 





