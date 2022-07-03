# Constness / Immutability


Don't

```
List<Repo> repos = getRepos();

int myRepoCount = 0;
for(Repo repo : repos) {
  if(repo.getOwner() == "me") {
    myRepoCount++;
  }
}
```



Do
  
```
import com.google.common.collect.ImmutableList;


final ImmutableList<Repo> repos = getRepos();

final int myRepoCount = repos.stream()
    .filter(repo -> repo.getOwner() == "me")
    .count();
```
