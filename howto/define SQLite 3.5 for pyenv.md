# 1. install sqlite 3.5

```
# Download the sqlite3 source code
wget https://www.sqlite.org/2021/sqlite-autoconf-3350500.tar.gz

# Extract the source code
tar xvfz sqlite-autoconf-3350500.tar.gz

# Go to the sqlite3 source code directory
cd sqlite-autoconf-3350500

# Configure the build
./configure

# Compile sqlite3
make

# Install sqlite3
sudo make install
```

note if got _c_type error in pip, need to install libffi-dev before pyenv install python 3.10
```
sudo apt-get install libffi-dev
```

# 2. reinstall pyhton 3.10
```
pyenv uninstall 3.10.13
PYTHON_CONFIGURE_OPTS="LD_RUN_PATH=/usr/local/lib LDFLAGS=-L/usr/local/lib" pyenv install 3.10.13
```

# 3. check version
```
import sqlite3
print(sqlite3.sqlite_version)
```

# 4. if not correct check which sqlite is used by python
```
ldd $(python -c "import _sqlite3; print(_sqlite3.__file__)") | grep sqlite3
```

e.g. `libsqlite3.so.0 => /lib/x86_64-linux-gnu/libsqlite3.so.0 (0x00007f87f6a07000)`


# 5. backup the sqlite and build soft link to the new sqlite

```
sudo mv /lib/x86_64-linux-gnu/libsqlite3.so.0 /lib/x86_64-linux-gnu/libsqlite3.so.0.backup
```

find libsqlite3.so.0 location, e.g. `/usr/local/lib` and use the path below. 

```
sudo ln -s /usr/local/lib/libsqlite3.so.0 /lib/x86_64-linux-gnu/libsqlite3.so.0
```



