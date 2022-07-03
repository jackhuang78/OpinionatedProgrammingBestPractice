# Constness and Immutability

## Motivation
Utilizing constness and immutability whenever possible reduces the number of mutable states that the readers need to keep in mind when parsing through one's code, thereby giving the readers a much easier time understanding the code correctly.

> **NOTE**: Newer langauges (e.g. Kotlin, Rust) often already provide support for this notion out of box via syntax or standard library. For older languages (e.g. Java, C++), adhering to this notion may produce more verbose code and require non-std (but well known and established) libraries.

## Examples

### Java

#### Don't

```
List<Repo> repos = getRepos();

int myRepoCount = 0;
for(Repo repo : repos) {
  if(repo.getOwner() == "me") {
    myRepoCount++;
  }
}
```

#### Do
  
```
import com.google.common.collect.ImmutableList;


final ImmutableList<Repo> repos = getRepos();

final int myRepoCount = repos.stream()
    .filter(repo -> repo.getOwner() == "me")
    .count();
```


### C++
#### Don't
```
std::vector<Repo> repos = GetRepos();

int myRepoCount = 0;
for(auto& repo : repos) {
  if(repo.owner == "me") {
    myRepoCount++;
  }
}
```

#### Do
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

