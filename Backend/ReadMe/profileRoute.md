we are going to show the profile only to those person that are `legal / authorized` meeans those people who are already sigin/up or those whose token is valid. main work is done with the help of middleware that is authenticateUser (authUser) over here basically we are decoding the token to get the user id 


## Q why user id 

bcz when we are creating the token we just have setted the user id in the token that's why when we decode it we only get the user id and then this user id will be used by us together with the userModel.findOne() to get the person whose token we have over here

```js
// during creating the token inside the model/user.model
userSchema.methods.generateAuthToken = function () {
    const token = jwt.sign({ _id: this._id }, process.env.JWT_SECRET, { expiresIn: '24h' }); // this expiery is ttl and it is reated to the logout route and token blackblisting 
    return token;
}
```
```js 
//decodin is done in the middleware/auth.midleware
  const decoded = jwt.verify(token, process.env.JWT_SECRET);
        const captain = await captainModel.findById(decoded._id)
        req.captain = captain;
        //not a complete middleware just a one portion of it 
```

## Download npm i 
cookieParser      it has the realtion with our token decodin throgh cookie 