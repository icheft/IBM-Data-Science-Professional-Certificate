# Introduction to Foursquare

+ Foursquare is a technology company that built a massive dataset of accurate location data.
+ Foursquare powers location data for Apple Maps, Uber, Snapchat, Twitter, and many others.
+ Their API and location data are currently being used by over 100,000 developers

Try out <https://foursquare.com/city-guide>.

# Using Foursquare API

## Search
`https://api.foursquare.com/v2/tips/CLIENTID...`

```
https://api.foursquare.com/v2/venues/client_id=*****&client_secret=*****&v=20210215&ll=40.73,-74.01&query=coffee
```

For a *venue* data, it contains:

+ Name
+ Unique ID
+ Location
+ Category

### More Detail
Can only make 500 similar calls per day (**`premium`** call).

```
https://api.foursquare.com/v2/venues/UNIQUEID?client_id=*****&client_secret=*****&v=20210215
```

+ ID
+ Name
+ URL
+ Contact Information
+ Statistics
+ Rating
+ Location
+ Tips


### Getting Tips

Only two tips will be returned per personal account.
```
https://api.foursquare.com/v2/venues/UNIQUEID/tips?client_id=*****&client_secret=*****&v=20210215
```

### Learning About a Specific User - API

```
https://api.foursquare.com/v2/users/USERID?client_id=*****&client_secret=*****&v=20210215
```

+ First Name
+ Last name
+ Gender
+ Contact Information
+ Friends
+ ID
+ Tips


## Explore and Other Queries

```
https://api.foursquare.com/v2/venues/explore?client_id=*****&client_secret=*****&v=20210215&ll=40.73,-74.01
```

`venue` data:

+ Name
+ Category
+ Unique ID
+ Location


### Exploring Trending Venues
```
https://api.foursquare.com/v2/venues/trending?client_id=*****&client_secret=*****&v=20210215&ll=40.73,-74.01
```

`venue`:

+ Name
+ Category
+ Name
+ Location

## Summary
1. Search for a specific type of venue around a given location - Regular
2. Learn more about a specific venue - **Premium**
3. Learn more about a specific Foursquare user - Regular
4. Explore a given location
5. Explore trending venues around a given location - Regular