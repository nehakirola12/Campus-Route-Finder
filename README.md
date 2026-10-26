# Campus Route Finder

A Python project that models a college campus as an **undirected, unweighted graph**
(locations = vertices, walkable paths = edges) and demonstrates **adjacency list /
adjacency matrix**, **BFS**, **DFS**, **shortest path by path reconstruction**,
**reachability** and **connected components**.

No external libraries are required (Python 3.8+). `Pillow` is needed only for
`make_screenshots.py`.

## Project structure
```
campus-route-finder/
├── main.py                  # CLI: interactive menu + single commands
├── src/
│   ├── graph.py             # CampusGraph (adjacency list) + AdjacencyMatrix
│   └── algorithms.py        # BFS, DFS (stack + recursive), reachability, components
├── data/campus_graph.txt    # Graph input: 11 locations, 13 paths
├── tests/test_cases.py      # Test cases (expected vs actual) + unittest
├── docs/REPORT.md           # Short report with complexity analysis
├── screenshots/             # PNG screenshots (+ .txt of the exact output)
└── make_screenshots.py      # Regenerates screenshots from real program output
```a

## How to run
```bash
python main.py                              # interactive menu
python main.py graph                        # adjacency list
python main.py matrix                       # adjacency matrix
python main.py bfs "Main Gate" Auditorium   # shortest route (BFS)
python main.py dfs Library                  # DFS traversal
python main.py reach "Main Gate"            # reachable + disconnected locations
python main.py compare                      # list vs matrix, BFS vs DFS
python main.py all-tests                    # expected vs actual table
python -m unittest tests.test_cases -v      # unit tests
```
Location names are case-insensitive. To change the campus, edit `data/campus_graph.txt`.

## Campus graph
Main Gate, Library, Block 1, Block 2, Cafeteria, Auditorium, Parking, Lab,
Admin Office, plus **Hostel** and **Sports Ground**, which are deliberately connected
only to each other to demonstrate a disconnected component.

## Sample output
```
$ python main.py bfs "Main Gate" Auditorium
BFS ROUTE: Main Gate -> Auditorium
------------------------------------------------------------
  Route : Main Gate -> Parking -> Cafeteria -> Auditorium
  Stops : 4 locations, 3 path(s) (minimum possible)
```
```
$ python main.py bfs "Main Gate" Hostel
BFS ROUTE: Main Gate -> Hostel
------------------------------------------------------------
  No route exists from Main Gate to Hostel (they are in different parts of campus).
```

## Test cases (expected vs actual)
```
ID  Case                     Expected                                             Actual                                               Result
--------------------------------------------------------------------------------------------------------------------------------------------
T1  Direct route             Main Gate > Library                                  Main Gate > Library                                  PASS
T2  Multi-stop route         Main Gate > Parking > Cafeteria > Auditorium         Main Gate > Parking > Cafeteria > Auditorium         PASS
T3  Unreachable              No route                                             No route                                             PASS
T4  Source == dest           Lab                                                  Lab                                                  PASS
T5  Multi-stop (3 edges)     Admin Office > Library > Block 1 > Lab               Admin Office > Library > Block 1 > Lab               PASS
T6  DFS reachable set        9 locations, no Hostel                               9 locations, Hostel in set: False                    PASS
T7  Connected components     2                                                    2                                                    PASS
--------------------------------------------------------------------------------------------------------------------------------------------
ALL TESTS PASSED
```

## Complexity summary
| | Time | Space |
|---|---|---|
| BFS (adj. list) | O(V + E) | O(V) |
| DFS (adj. list) | O(V + E) | O(V) |
| BFS / DFS (adj. matrix) | O(V²) | O(V) extra (O(V²) to store) |
| Adjacency list storage | – | O(V + E) |
| Adjacency matrix storage | – | O(V²) |

See `docs/REPORT.md` for the full explanation.

## GitHub
```bash
git init && git add . && git commit -m "Campus Route Finder: BFS/DFS on a campus graph"
git branch -M main
git remote add origin https://github.com/<your-username>/campus-route-finder.git
git push -u origin main
```
Repository link: `https://github.com/<your-username>/campus-route-finder`
