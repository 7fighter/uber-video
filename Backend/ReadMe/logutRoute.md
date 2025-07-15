all the people who will logout from their device their token will be moved to a new collection of data base called `blackListedtokenCollection` or idr sy phir token ki matching krty rahy gy jb v cookie yh phir header sy req ay gyi


if we start storing all the blackList token then db will get fulled so we start giving them the TTL (time to live) menas this from the db this specific collection will be removed after this time 


## logic 
perosn that logout's his token will be blaklisted and this blacklisted token will stay in our db for 24hrs bcz 86400 is given to expirey in our model/blacklistToken 
```js 
// model/blacklistToken 

const blacklistTokenSchema = new mongoose.Schema({
    token: {
        type: String,
        required: true,
        unique: true
    },
    createdAt: {
        type: Date,
        default: Date.now,
        expires: 86400 // 24 hours in seconds herer is ttl for staying in db
    }
});

module.exports = mongoose.model('BlacklistToken', blacklistTokenSchema);

```
so now when a person try login through the token our authmiddleware logic first match it with the the db collection of logout if it is in the blacklist then unauthorized access
```js
// middleware/authmiddleware
const isBlacklisted = await blackListTokenModel.findOne({ token: token });

    if (isBlacklisted) {
        return res.status(401).json({ message: 'Unauthorized' });
    }

```

`note` our token is valid for just 24 hrs not because hum naa db collection of blakclist main 86400 likh dyia it is beacsuse during creating the token we have given it the expiery time 24hrs 

```js 
// models/user.model
userSchema.methods.generateAuthToken = function () {
    const token = jwt.sign({ _id: this._id }, process.env.JWT_SECRET, { expiresIn: '24h' });  //valid for 24hrs
    return token;
}

```

### Short summary of above
login thorugh token is valid for 24hr after 24hrs perosn will login agian and new token will be issed. once the person click logout the token will be blacklisted and can't be used for the login. to save the storage this blacklisted token will be also deleted form the storage after 24hrs  