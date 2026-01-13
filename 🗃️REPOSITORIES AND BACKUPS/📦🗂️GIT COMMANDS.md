
## Set user and email

```
git config --global user.name "TuNombre"
```
```
git config --global user.email "tuemail@example.com"
```

## Sync folder with repository
```
git init
```
```
git remote add origin https://github.com/TuUsuario/TuRepositorio.git
```
Check what repository we are in
```
git remote -v
```
Delete repository stetted
```
git remote remove origin
```

## Upload new changes

```
git add .
```
```
git commit -m "Actualización de notas"
```
```
git push origin master
```

Verify commits created before
 ```
 git log  | git log --oneline
 ```

Return to a previous  commit
```
git reset --hard 7b8e120
```


## PULL REPOSITORY

This after set the user and the long link with the repository
```
git pull origin main
```







