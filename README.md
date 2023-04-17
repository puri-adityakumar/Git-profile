# Git-profile 🧑‍💻

## About the project
This is a simple JavaScript project that retrieves information about a GitHub user and displays it on a web page.  The user enters a GitHub username into a search box, and when they submit the form, the application makes an HTTP request to the GitHub API to retrieve the user's profile information and repository data.

If the user exists, the application displays the user's profile picture, name, bio, number of followers, following, and public repositories. It also shows the user's five most recently created repositories with links to them.

If the user doesn't exist, the application displays an error message.
The language that has been used to write this poject are HTML, CSS & JS. The original code used the Axios library to make HTTP requests to the GitHub API, while the modified code uses the fetch API to achieve the same functionality. 

## Here's a comparison of the changes made to the code and the original code side by side:

Original code
```
const { data } = await axios(APIURL + username);
```

Changed code :
```fetch(APIURL + username)
  .then(response => response.json())
  .then(data => {
    createUserCard(data);
    getRepos(username);
  })
  .catch(err => {
    if (err.response && err.response.status == 404) {
      createErrorCard("No profile with this username");
    }
  });
  ```

### Explanation:
Instead of using axios, I used fetch to make the HTTP request. The .then() method was used to parse the response as JSON and the .catch() method to catch any errors that may occur. To check for the response status in the error object, I used err.response.status instead of err.response && err.response.status, because fetch doesn't return an error object in the same way as axios. This allowed me to handle errors more consistently and reliably.

Original code
```
const { data } = await axios(APIURL + username + "/repos?sort=created");

```

Changed code

```
fetch(APIURL + username + "/repos?sort=created")
  .then(response => response.json())
  .then(data => {
    addReposToCard(data);
  })
  .catch(err => {
    createErrorCard("Problem fetching repos");
  });
  ```

### Explanation:
I replaced the axios function call with fetch to make the HTTP request. With fetch, I used the .then() method to parse the response as JSON and the .catch() method to catch any errors that may occur.
