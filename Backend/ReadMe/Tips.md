## Q1 After forking the project what cmd to run
as we dont have node module but we have package.json so running the 
```cmd
npm install 
```
it will download all tthe dependencies  

`note` make sure you are in the same directory (folder) for which you are going to run the cmd 


## Q2 using altas for the production  level is ok?
yes we can use it, 
but one issue of network acces might came that can be solved 
1. by going to the network acces that is son the left side 
2. and then adding an:

```
0.0.0.0/0
```
this will cerate an globall accesable ip address so that the issue of dynamic ip got solved             
## Q3 which errro is shown where

in the `vs code cmd` the `error `related to the `backend` is shown 
and in the browser cmd the error related to the frontend will be shown

### Q4 how the data base with the name test is created it can have differernt name but why test??
i think bcz we are directoly making a object or directly entering data might be bcz of that 
models yh schema  too bana rahy jis ki waja sy test data base ka andr name user, ride or captain a rahy or is ka andr  entaries in the form of document ja rahi

## Q5 /user/register kio /user/login kio??
for the context here we are talking about when we hitting we are writing 
```
http://localhost:4000/users/register
```
bcz 

```js
//app.js code
app.use("/users", userRoutes);
//over here /users dealing userRouter   
//look at the gdriveCopyProj folder webProj
```
## Q6 how to read the error 
the line that is like:
1. ```cmd
 /uber/backend/folde.....
    ```
2. under this line we will get the line bcz of which we will be facing the error and 
3. and under that it is written error: .....

from firsrt point we are getting the exact file addres where error is and through second point  we are getting the line which caused error.3rd point is the deatil of error  

## for runnig the app
```cmd
<!-- first install the nodemon -->
npx nodemon

<!-- or  -->
node server.js
```