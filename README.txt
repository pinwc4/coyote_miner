Miner and Pool for NRS
-----------------------------
This package includes a mining pool and miner for use with NRS.  The code is
very rough, but gets the job done.


Build
-----------------------------

git clone https://github.com/InvictusInnovations/BitShares.git bitshares
cd bitshares
git clone https://github.com/InvictusInnovations/fc.git
cd ..
cmake . -DCMAKE_BUILD_TYPE=Release
make

You may want to make sure cmake is in Release mode.


Usage
------------------------

./pool_miner HOST:PORT WORKERNAME [OPTIONAL THREAD NUMBER]

