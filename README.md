# Python Repo Analyser

A Python project that analyzes public GitHub repositories using the GitHub REST API. It retrieves repository data, calculates statistics, ranks repositories, and allows users to search for specific repositories.

## Features

- **GitHub API Integration:** Fetches public repositories for a specified GitHub username.
- **Automatic Pagination:** Retrieves repositories across multiple pages.
- **Repository Statistics:** Displays repository names, programming languages, stars, and sizes.
- **Language Analysis:** Counts repositories by programming language.
- **Star Analysis:** Calculates the total stars across repositories.
- **Repository Ranking:** Sorts repositories by stars and size.
- **Ratio Analysis:** Calculates the star-to-size ratio for repositories with non-zero size.
- **Repository Search:** Searches for repositories by name, ignoring letter case.
- **Error Handling:** Handles invalid usernames, HTTP errors, and request timeouts.
- **Empty Results Handling:** Handles users with no public repositories.

## Technologies Used

- Python
- Requests library
- GitHub REST API
- JSON
- Dictionaries, lists, loops, and functions

## Requirements

- Python 3
- `requests` library
- Internet connection

## Installation

Install the required library:

```bash
pip install requests