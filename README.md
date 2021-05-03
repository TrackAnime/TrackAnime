Original App Design Project - README Template
===

# TrackAnime

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
2. [Schema](#Schema)

## Overview
### Description
An app that provides a list of anime, along with genres and ratings. You'll be able to keep tabs on what anime you have watched, what you're watching, and what you might be interested in.

### App Evaluation
- **Category:** Anime / Entertainment
- **Mobile:** Mobile is a necessary device in order for the user to immediately keep tabs on their shows.
- **Story:** Allows either users that watch too many shows or those that watch every couple of months after to track whatever they are watching. Since it's a private experience as of now, users can be relaxed that no one can view their list.
- **Market:** For anyone that has an interest in anime and want to keep track of their evergrowing list.
- **Habit:** Users can explore countless anime by browsing the app and find one they have an interest on.
- **Scope:** For now, this app is meant for the individual. Eventually, it will serve to have some kind of social interaction between the users.

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

* User can create a new account
* User can login
* User can browse through all sorts of anime
* User can view anime summary, genre, and ratings
* User can keep tabs on what they're watching, on what they are interested in, and what they've watched already.
* User can logout

**Optional Nice-to-have Stories**

* Users can see a top 10 list
* Users can see a trending page
* Users can write a review
* Users can see a list of other users
* Users can enable dark mode
* Users can do a quiz to see how knowledgeable they are

### 2. Screen Archetypes

* Login / Signup screen
   * User can login
   * User can create a new account
* Stream
   * User can browse through a feed of anime
* Detail / Overview
   * User can view genre, rating, and summary of the show
   * User can tap on three buttons to show whether they they have watched it, are watching it, or have an interest, respectively
* Watching List
   * User can see the list of anime they are watching
* Completed List
   * User can see the list of anime they have completed
* Interested List
   * User can see the list of anime they are interested in
* Settings
   * User can logout

### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Stream
* Watching List
* Completed List
* Interested List
* Settings

**Flow Navigation** (Screen to Screen)

* Login / Signup screen 
   * Stream
* Stream screen
   * Detail / Overview
* Watching List
   * Detail / Overview
* Completed List
   * Detail / Overview
* Interested List
   * Detail / Overview
* Settings
   * Login / Signup screen

## Wireframes
<img src="https://i.imgur.com/UupoYfv.jpg" width=600>

## Schema 
[This section will be completed in Unit 9]
### Models
#### User

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | objectId      | String   | unique id for the user (default field) |
   | username       | String | name of the user |
   | password      | String | password of the user |
   | createdAt     | Date | date when post is created (default field) |
   | updatedAt     | Date | date when post is last updated (default field) |

### Networking
#### List of network requests by screen
   - Login/Signup Screen
      - Login 
          - private void loginUser(String username, String password) {
        Log.i(TAG, "Attempting to login user " + username);
        // TODO: navigate to the main activity if the user has signed in properly
        ParseUser.logInInBackground(username, password, new LogInCallback() {
            @Override
            public void done(ParseUser user, ParseException e) {
                if (e != null) {
                    // TODO: better error handling
                    Log.e(TAG, "Issue with login", e);
                    Toast.makeText(LoginActivity.this, "Issue with login!", Toast.LENGTH_SHORT).show();
                    return;
                }
                // TODO: navigate to the main activity if the user has signed in properly
                goMainActivity();
                Toast.makeText(LoginActivity.this, "Success!", Toast.LENGTH_SHORT).show();
            }
        });
    }
      - Signup
          - private void signUpUser() {
        // Create the ParseUser
        ParseUser user = new ParseUser();
        // Set core properties
        user.setUsername(etUsername.getText().toString());
        user.setPassword(etPassword.getText().toString());
        // Invoke signUpInBackground
        user.signUpInBackground(new SignUpCallback() {
            public void done(ParseException e) {
                if (e == null) {
                    // Hooray! Let them use the app now.
                    goMainActivity();
                    Toast.makeText(LoginActivity.this, "Success!", Toast.LENGTH_SHORT).show();
                } else {
                    // Sign up didn't succeed. Look at the ParseException
                    // to figure out what went wrong
                    Log.e(TAG, "Issue with signup!", e);
                    Toast.makeText(LoginActivity.this, "Issue with signup!", Toast.LENGTH_SHORT).show();
                    return;
                }
            }
        });
    }
