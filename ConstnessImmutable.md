# Constness / Immutability

## Java

### Don't

```
List<Repo> repos = getRepos();

int myRepoCount = 0;
for(Repo repo : repos) {
  if(repo.getOwner() == "me") {
    myRepoCount++;
  }
}
```

### Do
  
```
import com.google.common.collect.ImmutableList;


final ImmutableList<Repo> repos = getRepos();

final int myRepoCount = repos.stream()
    .filter(repo -> repo.getOwner() == "me")
    .count();
```


## C++
### Don't
```
std::vector<Repo> repos = GetRepos();

int myRepoCount = 0;
for(auto& repo : repos) {
  if(repo.owner == "me") {
    myRepoCount++;
  }
}
```

### Do
```
const std::vector<Repo> repos = GetRepos();

const int myRepoCount = [&](){
  int count = 0;
  for(const auto& repo : repos) {
    if(repo.owner == "me") {
      count++;
    }
  }  
  return count;
}();

```

