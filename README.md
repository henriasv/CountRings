#Ring Statistics Algorithm
##Counting policy

* Count only irreducible rings (rings not having shortcut bridges).
* Count rings purely topologically. Do not use geometrical information.
* Edge direction is not considered. (Undirected graph)

##Algorithm

1. Choose 3 successive nodes along the network.
1. Find the smallest rings passing the three nodes.
1. The ring must not have shotcuts, i.e. path connecting two vertices on the ring which is shorter than the 1. 1. path along the ring. (Using Dijkstra's algorithm.)
1. Put the ring in the list.
1. Repeat 1 .. 4 until all sets of 3 successive nodes are tested.
1. Eliminate the permutations of a ring in the list.
1. (Optional) Remove "crossing rings".

##Usage
Input data must be in @NGPH format. Output data will be in @RNGS format.

    % ./countrings3.py 8 < test.ngph > test.rngs
    % ./countrings3.py 8 < test.ngph | ./crossingrings.pl > test2.rngs

##Sample
The following is the expression of a cubic graph, which should have six 4-cycles.

    @NGPH
    8
    0 1
    1 2
    2 3
    3 0
    4 5
    5 6
    6 7
    7 4
    0 4
    1 5
    2 6
    3 7
    -1 -1

You can pick up many samples at the Vitrite database:
    http://vitrite.chem.okayama-u.ac.jp
##Known Problems
###Sample 1
Number of rings in this kind of graph consisting of N bows is counted as N (N-1) / 2. It happens because of the lack of 3-dimentional geometrical information.
###Sample 2
It is a smaller version of sample 1 consisting of 4 bows. As you see, surface rings of this structure seems to be 4, while the algorithm counts as 6, because it also counts the “crossing rings” (diagonal red and blue rings). These sample topologies rarely appear in the network of water at low temperature because the z-index at the top and bottom nodes is too large. 
While, there is another sample containing crossing rings but still undistorted.
Sample 3
##Wayarounds
The small Perl program “crossingrings.pl” looks up all the crossing rings in the ring list (in @RNGS format) and remove one of them randomly until the crossing is avoided. With the use of 3-dimentional geometrical information, there might be better walkarounds.