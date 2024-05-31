Social Network - System Design

Social nerwork project is a social network for travelers.

### Functional requirements:

- add posts;
- comment posts;
- rate posts;
- subscribe on another users;
- search posts from popular places, filter by country, city;
- direct chats;
- viewing the feeds of another users.

### Non-functional requirements:

- 10 000 000 DAU
- availability 99,95%
- geo distribution is not needed
- syncronize sessions on different devices (mobile, web)
- seasonality in the application

### Basic calculations

RPS (add/read post):
```
DAO = 10 000 000
Read_operations ~= 5 day
Write_operatioons ~= 1 month

RPS (read) = 10 000 000 / 86 400 * 5 = 579
RPS (write) = 10 000 000 / 86 400 / 30 = 4 
```

Post size:
```
Post
 - ID           int64
 - UserID       int64
 - Message      string
 - Created      time.Datetime
 - Coordinates  float64 * 2
 - ImageUrls    []string
 
Post =  8 + 8 + 200 * 4 + 24 + 16 + 5 * 1 * 100 = 1356B ~= 1.5Mb
```

Traffic:
```
Traffic (read) = 579 * 2 ~= 1160Mb/s
Traffic (write) = 4 * 2 ~= 8Mb/s
```

Required memory for posts:
```
Replication factor = 3
Service operation time = 5 years
Created posts for 5 years = 10 000 000 / 30 * 365 * 5 ~= 608 333 333
Each record size for a post ~= 1356B 
Required memory for 5 years = 608 333 333 * 1356 * 3 = 2 474 699 998 644 ~= 2474TB
```
