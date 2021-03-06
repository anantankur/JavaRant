# JavaRant
A devRant API wrapper for Java.

[![Maven Central][mavenCentralShield]][mavenCentral]
[![Jenkins][jenkinsBuildShield]][jenkins]
[![Jenkins tests][jenkinsTestsShield]][jenkinsTests]

[mavenCentralShield]: https://img.shields.io/maven-central/v/com.scorpiac.javarant/javarant.svg
[jenkinsBuildShield]: https://img.shields.io/jenkins/s/https/jenkins.scorpiac.com/job/LucaScorpion/job/JavaRant/job/master/.svg
[jenkinsTestsShield]: https://img.shields.io/jenkins/t/https/jenkins.scorpiac.com/job/LucaScorpion/job/JavaRant/job/master/.svg
[mavenCentral]: https://mvnrepository.com/artifact/com.scorpiac.javarant/javarant
[jenkins]: https://jenkins.scorpiac.com/job/LucaScorpion/job/JavaRant/
[jenkinsTests]: https://jenkins.scorpiac.com/job/LucaScorpion/job/JavaRant/job/master/lastCompletedBuild/testReport/

## Maven
JavaRant is available on [Maven][mavenCentral], simply add this dependency to your `pom.xml` file:

```xml
<dependency>
	<groupId>com.scorpiac.javarant</groupId>
	<artifactId>javarant</artifactId>
	<version>2.1.0</version>
</dependency>
```

## Using JavaRant

To access devRant simply create a new `DevRant` object:

```
DevRant devRant = new DevRant();
```

The `DevRant` class itself can be used to get specific rants and users.

```
// Get a specific rant.
CommentedRant rant = devRant.getRant(686001);

// Get a user by username.
User me = devRant.getUser("LucaScorpion");
```

The `DevRant` class contains 2 methods for getting to specific parts of the api.
First, `getFeed()` which returns a `DevRantFeed` object.
This is used to access the rant and collab feeds.

```
// Get the 10 latest rants.
List<Rant> recent = devRant.getFeed().getRants(Sort.RECENT, 10, 0);

// Get the 10 best stories.
List<Rant> stories = devRant.getFeed().getStories(Sort.TOP, 0);

// Get 10 collabs.
List<Collab> collabs = devRant.getFeed().getCollabs(10);
```

Second, `getAuth()` which returns a `DevRantAuth` object, which is used to access user functionality.
Note that a user needs to be logged in before this can be accessed.

```
// Log in to devRant.
char[] password = "<password>".toCharArray();
devRant.login("<username>", password);

// Upvote a rant.
devRant.getAuth().voteRant(832125, Vote.UP);

// Clear the vote on a comment.
devRant.getAuth().voteComment(832169, Vote.NONE);

// Log out to clear the token.
devRant.logout();
```
