# Design Plan

**Architecture**

Web Browser, C# Class Library

Web Server / Https

Used Xml Serialization to Persist Objects

**Web Server Interface**

- System (static)

 -List <Person> RegisteredUsers

 +LoadFromFile()
 
 +SaveToFile()
 
 +RegisterNewUser()
 
 +ClearAllData()

- Person

 -Username
 
 -Password
 
 -FirstName
 
 -LastName
 
 -Friends
 
 -Wall
 
 -FriendRequestsReceived
 
 -FriendRequestsSent

- Post

 -PostDate
 
 -Subject
 
 -Body
 
 -Author

- User

 -Self
 
 +Constructor(Person thisUser)
 
 +Authenticate(string username, string password)
 
 +ComposePost(string Subject, string body, Person postingTo)
 
 +SendFriendRequest(Person requestedPerson)
 
 +RespondToFriendRequest(Bool is Confirmed, Person sentBy)
 
 +ViewWall(Person personToView)
 
 +ViewPost(Post postToView)
 
 +ViewAllUsers()
 
 +ViewFriends()
 
 +ViewSentFriendRequests()
 
 +ViewReceivedFriendRequests()

**Functions**

- System

 +LoadFromFile()
 Xml Serializer crawls all objects contained within the Registered Users system property and persists them to xml file within a directory.
 
 +SaveToFile()
 Deserializes xml into objects and puts into memory.
 
 +RegisterNewUser()
 add a new user object to the RegisteredUser system property.
 
 +ClearAllData()
 deletes all xml within the directory

- User
 +Constructor(Person thisUser)
 a new User object will be constructed to have a Person as the self property to represent the logged in user.
 
 +Authenticate(string username, string password)
 checks if the credentials match one in the RegisteredUsers system property.
 
 +ComposePost(string Subject, string body, Person postingTo)
 makes a new post with this.self as the author. adds it to the postingTo Person's wall (List of Posts)
 
 +SendFriendRequest(Person requestedPerson)
 adds the requested person to both lists: this users sentfriendrequests, and the requestedPersons receivedfriendrequests
 
 +RespondToFriendRequest(Bool is Confirmed, Person sentBy)
 checks if the Person is not already a friend, and if they have a pending request received. 
 if so adds both users to eachother's friends lists
 
 +ViewWall(Person personToView)
 returns a List of Posts of that person's wall
 
 +ViewPost(Post postToView)
 can only view if person is friends otherwise sends error message.
 returns an interpolated string of the post's details
 
 +ViewAllUsers()
 returns an interpolated string of each User's details within the RegisteredUsers System Property
 
 +ViewFriends()
 returns an interpolated string of all of the Persons within the user's friendlist
 
 +ViewSentFriendRequests()
 returns an interpolated string of all of the Persons within the user's Sent friend Requests
 
 +ViewReceivedFriendRequests()
 returns an interpolated string of all of the Persons within the user's Received friend Requests
	
