# Acceptance Testing the Planetarium Application
Instead of going case-by-case, I will start by proceeding screen by screen, acting as an End User and then afterwards, going through the use-cases.

## Login Screen
1. The access point for this application does not inspire confidence to an end user
   2. This is due to having a localhost url - normally it would identify the organization that the site is advertising
   3. As a developer, we would notice that it does not start with https so naturally we feel it is not secure
2. Password is hidden which does inspire confidence

## Register Screen
1. There is no back button to the Login screen
   2. While the audience that is using this application is likely to understand how to get back to the login, you cannot
   assume that this is the case (**Risky**)
3. Upon successful or unsuccessful register, an alert pops up that reveals your password (**Severe**)
   4. Also, there is no redirect back to the login

## Planetarium Home Page
I will split this into three parts: the screen itself, the add functionality, and the remove functionality.

### Planetarium Screen
1. The logout button is tiny in the top right corner. It is easy to miss.

### Remove Functionality
1. At first glance, it appears to be simple, but it does have some dangerous abilities since 
you can remove other user's planets and moons (**Severe**)

### Add Functionality
1. You have to include a valid image to submit a planet or moon
   2. This image must be in the form of jpeg (**Inconvenient**)
3. Adding a moon shows up in every user's Planetarium (**Severe**)
4. Adding planets that share the same name of another user's planet is rejected
   5. The alert that pops up doesn't tell me anything helpful other than I can't use that name

## Styling
While the Planetarium home page has a background, the login and register screens do not.
Including a uniform background can inspire confidence as far as styling goes. 

# Screen Summary
Ultimately, I found confused when I was in the Planetarium home page. The whole concept of ownership, 
when implemented correctly makes sense. Here it does not. If unique names for planets and moons
are required across their respective tables, then users will hit that specific issue relatively often. 
Many astrologists / space enthusiasts will be tracking and studying the same planets and moons so
why require uniqueness. Or, if you do require it, make it specific to a user's planetarium. Also,
the way we see Owner ID and Planet/Moon ID also feels redundant. If planet names are unique, then
we should be able to assign it to the planet and that would create some sort of dropdown where thtat planet
is and will hold the newly created moon.

# Acceptance Testing by Use-Cases
## ID = 1: Users should be able to open a new User account with the Planetarium
1. Passwords must be obfuscated when registering for an account
    - Positive Testing: Failed (Alert pops up upon successful account registration that reveals password in plain text)
    - Negative Testing: Failed (Alert pops up upon unsuccessful account registration that reveals password in plain text)

## ID = 2: Users should be able to securely access their account
1. Passwords must be obfuscated when logging into their account
    - Positive Testing: Passed (checked the console)
    - Negative Testing: Passed (checked the console)

## ID = 3: Users should be able to see planets and moons added to the Planetarium
Given the user with {username} and {password} logs in successfully, they should see their username in the header at the
top of the page
- Acceptance Testing: Passed (name was reflected in the header)

## ID = 4 - Users should be able to add new planets to the Planetarium
Given the user has added a planet with {planet_name}, it should be reflected in the planetarium
- Passed (planets can be seen and stay even if you log out and log back in)

## ID = 5 - Users should be able to remove planets from the Planetarium
Requirement: Users should only be able to interact with resources they have added to the Planetarium
- Positive Testing: Passed (planet was removed from {username}'s planetarium)
- Negative Testing: Failed (planet with {planet_name} was removed from {other_user_name}'s planetarium)

## ID = 6 - Users should be able to add Moons to the Planetarium associated with a planet
Given a {user} adds a Moon to their planetarium, will {userX} see said moon in their table?
- Failed (Moons can be seen across user accounts)
  - They appear to be treated globally

## ID = 7 - Users should be able to remove moons from the Planetarium
Given a {user} removes their own Moon from the planetarium, will {userX} have said moon removed from their table?
- Failed (Moons are global, so they're removed across accounts)

## Use-Case Acceptance Testing Summary Table

| Passed | Failed |
|--------|--------|
| 5      | 5      |


