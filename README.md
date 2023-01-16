# fly-pub

Deploy [pub](https://github.com/davecheney/pub) in fly.io


1. Set up mariadb fly app
  ```
  cd mariadb
  fly launch # Don't deploy and revert changes applied by to fly.toml
  fly secrets set \
    MARIADB_PASSWORD=<MARIADB_PASSWORD> \
    MARIADB_ROOT_PASSWORD=<MARIADB_ROOT_PASSWORD>
  fly volumes create pubdata
  fly deploy
  ```
2. Set up pub fly app
  ```
  cd serve
  fly launch # Don't deploy yet
  fly secrets set 'DSN=pub:<MARIADB_PASSWORD>@tcp(pub-mariadb.internal:3306)/pub'
  fly deploy
  ```
3. Follow [Setup](https://github.com/davecheney/pub#setup) instructions from pub. Connect to the remote database by running a proxy:
  ```
  fly proxy 3306 -a pub-mariadb
  ```
