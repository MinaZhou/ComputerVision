Stitching in OpenCV:
https://docs.opencv.org/2.4/modules/stitching/doc/stitching.html

I focus on the seam estimation algorithm recently.

class CV_EXPORTS SeamFinder{
public:
    virtual ~SeamFinder() {}
    virtual void find(const std::vector<Mat> &src, const std::vector<Point> &corners,
                      std::vector<Mat> &masks) = 0;
};

class CV_EXPORTS GraphCutSeamFinderBase
{
public:
    enum { COST_COLOR, COST_COLOR_GRAD };
};

class CV_EXPORTS GraphCutSeamFinder : public GraphCutSeamFinderBase, public SeamFinder
{
public:
    GraphCutSeamFinder(int cost_type = COST_COLOR_GRAD, float terminal_cost = 10000.f,
                       float bad_region_penalty = 1000.f);

    void find(const std::vector<Mat> &src, const std::vector<Point> &corners,
              std::vector<Mat> &masks);

private:
    /* hidden */
};`

https://github.com/opencv/opencv/blob/master/modules/stitching/src/seam_finders.cpp

theory:

Cut (graph theory)
From Wikipedia, the free encyclopedia

In graph theory, a cut is a partition of the vertices of a graph into two disjoint subsets. Any cut determines a cut-set, the set of edges that have one endpoint in each subset of the partition. These edges are said to cross the cut. In a connected graph, each cut-set determines a unique cut, and in some cases cuts are identified with their cut-sets rather than with their vertex partitions.

In a flow network, an s–t cut is a cut that requires the source and the sink to be in different subsets, and its cut-set only consists of edges going from the source's side to the sink's side. The capacity of an s–t cut is defined as the sum of the capacity of each edge in the cut-set.

A cut is minimum if the size or weight of the cut is not larger than the size of any other cut. The illustration on the right shows a minimum cut: the size of this cut is 2, and there is no cut of size 1 because the graph is bridgeless.

The max-flow min-cut theorem proves that the maximum network flow and the sum of the cut-edge weights of any minimum cut that separates the source and the sink are equal. There are polynomial-time methods to solve the min-cut problem, notably the Edmonds–Karp algorithm.[1]

reference:
[http://www.cs.utexas.edu/~grauman/courses/fall2011/handouts/examples/Adrian_demo_with_notes.pdf](http://www.cs.utexas.edu/~grauman/courses/fall2011/handouts/examples/Adrian_demo_with_notes.pdf)

