
```
docker ps -a | grep kpmg | awk '{print $1}' | xargs -I {} touch {}
```