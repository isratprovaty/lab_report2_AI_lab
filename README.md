# lab_report2_AI_lab
def iddfs(maze, start, target, max_depth):
    rows, cols = len(maze), len(maze[0])
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)] 

    def dls(node, depth, path):
        if node == target:
            return path + [node]
        if depth == 0:
            return None
        
        x, y = node
        for dx, dy in directions:
            nx, ny = x + dx, y + dy
            if 0 <= nx < rows and 0 <= ny < cols and maze[nx][ny] == 0 and (nx, ny) not in path:
                result = dls((nx, ny), depth - 1, path + [node])
                if result:
                    return result
        return None

    for depth in range(max_depth + 1):
        path = dls(start, depth, [])
        if path:
            print(f"Path found at depth {depth} using IDDFS")
            print("Traversal Order:", path)
            return
    
    print(f"Path not found at max depth {max_depth} using IDDFS")


if __name__ == "__main__":
    
    case1_maze = [[0, 0, 1, 0], [1, 0, 1, 0], [0, 0, 0, 0], [1, 1, 0, 1]]
    case1_start = (0, 0)
    case1_target = (2, 3)
    max_depth = 6 
    
    iddfs(case1_maze, case1_start, case1_target, max_depth)
    
    case2_maze = [[0, 1, 0], [0, 1, 0], [0, 1, 0]]
    case2_start = (0, 0)
    case2_target = (2, 2)
    
    iddfs(case2_maze, case2_start, case2_target, max_depth)
