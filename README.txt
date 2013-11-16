Miner and Pool for ProtoShares
-----------------------------
This package includes a mining pool and miner for use with ProtoShares.  The code is
very rough, but gets the job done.


Build
-----------------------------

git clone https://github.com/InvictusInnovations/BitShares.git bitshares
cd bitshares
git clone https://github.com/InvictusInnovations/BitShares.git fc
cmake . -DCMAKE_BUILD_TYPE=Release
make

You may want to make sure cmake is in Release mode.


Usage
------------------------

./gw_miner HOST USER PASS

