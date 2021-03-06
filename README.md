# sfmt-dist

sfmt distribution

STANDARD INTERFACE
==================
std::uniform_int_distribution and std::normal_distribution adaptable
SFMT19937

sample code
-----------
    std::uniform_int_distribution<uint32_t> dist(0, 200);
    MersenneTwiseter::SFMT19937 sfmt(1234);
    cout << dec << dist(sfmt) << endl;

ORIGINAL INTERFACE FOR dSFMT
============================
original distribution MersenneTwister::UniformIntFromDouble and
MersenneTwister::NormalFromDouble for DSFMT19937

sample code
-----------
    using MersenneTwister::NormalFromDouble;
    using MersenneTwister::DSFMT19937;
    NormalFromDouble<DSFMT19937> dist(0.0, 1.0, 1234);
    cout.setf(std::ios::fixed);
    for (uint64_t i = 0; i < 100; ++i) {
        cout << dec << setprecision(20) << dist() << endl;
    }

    using MersenneTwister::UniformIntFromDouble;
    UniformIntFromDouble<uint32_t, DSFMT19937> dist(0, 200, 1234) ;
    cout.setf(std::ios::fixed);
    for (uint64_t i = 0; i < count; ++i) {
        cout << dec << dist() << endl;
    }

TEST PROGRAM
============

"make check" does internal check
--------------------------------
test_mt19937, test_sfmt19937, test_dsfmt19937, test_mt19937_64
checks their outputs matches official test vectors.

output and speed
----------------
non installed programs "output" and "speed" are programs that users
can check outputs and measure speed.

    ./output
    ./output [-n|-u] [-m|-M|-S|-d] [-s seed] [-c count] [-f start] [-l end]
    -n --normal   normal distribution
    -u --uniform  uniform distribution
    -m --std-mt   std::mersennetwister19937
    -M --mt-mt    MersenneTwister19937
    -S --sfmt     SFMT19937
    -d --dsfmt    dSFMT19937
    -s --seed     seed
    -c --count    count
    -f --start    start of uniform range
    -l --end      end of uniform range

    ./output -u -S -f100 -l200 -c 10 -s 2
    #uniform distribution[100,200] :MersenneTwister::SFMT19937
    128
    152
    100
    141
    175
    170
    144
    198
    111
    164

    ./speed
    ./speed [-n|-u] [-m|-M|-S|-d] [-s seed] [-c count] [-f start] [-l end]
    -n --normal   normal distribution
    -u --uniform  uniform distribution
    -m --std-mt   std::mersennetwister19937
    -M --mt-mt    MersenneTwister19937
    -S --sfmt     SFMT19937
    -d --dsfmt    dSFMT19937
    -s --seed     seed
    -c --count    count
    -f --start    start of uniform range
    -l --end      end of uniform range

    ./speed -u -S
    #uniform distribution[0,200] time for 100000000 generation
    MersenneTwister::SFMT19937,868ms
    ./speed -u -d
    #uniform distribution[0,200] time for 100000000 generation
    MersenneTwister::dSFMT19937,168ms
