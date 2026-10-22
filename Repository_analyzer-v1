import requests
#guthub repository analyser
print("==WELLCOME TO GITHUB REPOSITORY ANALYSER==")
#take userinput
username = input("Enter the GitHub username:").strip()
#github url
url = f"https://api.github.com/users/{username}/repos"
#handle error
try:
    all_repos = []
    page=1

    while True:
      response = requests.get(
          url,
          params={"per_page": 10, "page": page},
          timeout=10
      )
      response.raise_for_status()

      repos = response.json()
      if not repos:
        break
      else:  
        all_repos.extend(repos)
        page+=1

    repos = all_repos
    repository_list=[]

    print("==REPOSITORY DETAILS==")
#show repository name, language,star,size
    for repo in repos:
        print("Name:", repo["name"])
        print("Language:", repo["language"])
        print("Stars:", repo["stargazers_count"])
        print("size:",repo["size"],"KB")
        repo_lower=repo["name"].lower()
        repository_list.append(repo_lower)
        print("-" * 25)
#to store language with it counts in the form of dictionary 
    language_counts = {}
    stars=0
#to store the stars counts with its repository name
    repository_dict={}
#to store the size with its repository name
    repo_size_dict={}
#sort repository language and its counts
    for repo in repos:
       language = repo["language"]
       star=repo["stargazers_count"]
       size=repo["size"]
       repository_dict[repo["name"]]=star
       repo_size_dict[repo["name"]]=size
       stars+=star

       if language is not None:
         if language in language_counts:
            language_counts[language] += 1
         else:
            language_counts[language] = 1

    if len(repository_dict)==0:
      print("no repository found in this GitHub profile ")
    else:
      max_value=max(repository_dict,key=repository_dict.get)
      max_size=max(repo_size_dict,key=repo_size_dict.get)
      min_size=min(repo_size_dict,key=repo_size_dict.get)
      sorted_value=sorted(repo_size_dict,key=repo_size_dict.get,reverse=True)
      sorted_value_=sorted(repository_dict,key=repository_dict.get,reverse=True)
      max_repo_size=repo_size_dict[max_size]
      min_repo_size=repo_size_dict[min_size]
      max_star=repository_dict[max_value]

      print("==REPOSITORY SIZE==")
#show the repository size
      for i in sorted_value:
        print(f"{i}:{repo_size_dict[i]} KB")
      print("-"*25)
      print("==REPOSITORY STARS==")
#show the repository stars
      for i in sorted_value_:
        print(f"{i}:{repository_dict[i]} stars")
      print("-"*25)
#github summary
      print("====GITHUB SUMMARY REPORT====")
#show the total number of repository 
      print("Total repositories:",len(repos))
#show number of repository in each language 
      for i in language_counts:
        print(f"{i} repositories:{language_counts[i]}")
#show total stars or rating of the profile 
      print("Total stars:",stars)
#create a list to store largest repository size
      largest_repo_list=[]
#show all the largest size repository 
      for i in repo_size_dict:
        if max_repo_size==repo_size_dict[i]:
            largest_repo_list.append(i)
      print(f"Largest repository: {','.join(largest_repo_list)}({repo_size_dict[largest_repo_list[0]]}KB)")
#create a list to store least repository size
      smalest_repo_list=[]
#show all the smallest size repository 
      for i in repo_size_dict:
        if min_repo_size==repo_size_dict[i]:
            smalest_repo_list.append(i)
      print(f"Least repository: {','.join(smalest_repo_list)}({repo_size_dict[smalest_repo_list[0]]}KB)")
#create a list to store most stared repository   
      starlist=[]
#show all the most stared repository 
      for i in repository_dict:
        if max_star==repository_dict[i]:
            starlist.append(i)
      if repository_dict[starlist[0]]<=1:
       print(f"Most-stared repository: {','.join(starlist)} ({repository_dict[starlist[0]]} star each)")
      else:
       print(f"Most-stared repository: {','.join(starlist)} ({repository_dict[starlist[0]]} stars each)")
#create a list to store lowest stared repository
      min_starlist=[]
#show all the lowest stared repository 
      min_value=min(repository_dict,key=repository_dict.get)
      min_star=repository_dict[min_value]
      for i in repository_dict:
        if min_star==repository_dict[i]:
            min_starlist.append(i)
      if repository_dict[min_starlist[0]] <=1:
        print(f"Least-stared repository: {','.join(min_starlist)} ({repository_dict[min_starlist[0]]} star each)")
      else:
        print(f"Least-stared repository: {','.join(min_starlist)} ({repository_dict[min_starlist[0]]} stars each)")
#create a dictionary to store the star-size ratio with its name 
      rating_ratio={}
#find the star-size ratio for each repository 
      for repo in repository_dict:
        if repo_size_dict[repo]>0:
          ratio=repository_dict[repo]/repo_size_dict[repo]
          rating_ratio[repo]=ratio
#find the maximum star-size ratio
      if len(rating_ratio)==0:
        print("There is no star-size ratio.")
      else:
        max_ratio=max(rating_ratio,key=rating_ratio.get)
#find the minimum star-size ratio
        min_ratio=min(rating_ratio,key=rating_ratio.get)
#create a list to store largest star-size ratio repository
        largest_ratio_list=[]
#create a list to store smallest star-size ratio repository
        lowest_ratio_list=[]
#show all the largest star-size ratio repository 
        for i in rating_ratio:
          if rating_ratio[max_ratio]==rating_ratio[i]:
            largest_ratio_list.append(i)
        print(f"Largest star-size ratio: {','.join(largest_ratio_list)}({rating_ratio[largest_ratio_list[0]]})")
#show all the smallest star-size ratio repository 
        for i in rating_ratio:
          if rating_ratio[min_ratio]==rating_ratio[i]:
            lowest_ratio_list.append(i)
        print(f"Lowest star-size ratio: {','.join(lowest_ratio_list)}({rating_ratio[lowest_ratio_list[0]]})")
        print("==FILTER REPOSITORY==")
        while True:         
          repo_name=input("Enter the repository name:").strip()
          if repo_name.lower()=="exit":
            break
          elif repo_name.lower() in repository_list:
           for  repo in repos:
             if repo_name.lower()==repo["name"].lower():
              print("Name:",repo["name"])
              print("Language:",repo["language"])
              print("Stars:",repo["stargazers_count"])
              print("size:",repo["size"],"KB")
              print("-" * 25)
              break
          else:
              print("repository not found.")
 #handle http error
except requests.exceptions.Timeout:
    print("Request Timed out.please try again.")
except requests.exceptions.HTTPError as e:
    if response.status_code==404:
      print("GitHub username not found.")
    else:
      print("Httprror:", e)
#handle requestexception error
except requests.exceptions.RequestException as e:
    print("Request failed:", e)