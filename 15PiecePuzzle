def IsSolvable(puz):

        Inversions = InversionsCounter(puz)
        blank_position = _get_blank_space_row_counting(puz)

        if IsEven(blank_position) and IsOdd(Inversions):
            return True
        elif IsOdd(blank_position) and IsEven(Inversions):
            return True
        else:
            return False
            
def InversionsCounter(puz):

        inv_count = 0
        puzzle_list = [number for row in puz for number in row if number != 0]
        for i in range(len(puzzle_list)):
            for j in range(i + 1, len(puzzle_list)):
                if puzzle_list[i] > puzzle_list[j]:
                    inv_count += 1
        return inv_count


def IsOdd(num):
    return num % 2 != 0

def IsEven(num):
    return num % 2 == 0


def _get_blank_space_row_counting(puz): 

    zero_row, _ = IndexPosition(0,puz)  
    return ROWS - zero_row


def swap(puz, x1, y1, x2, y2):

        copy = [list(row) for row in puz]  
        copy[x1][y1], copy[x2][y2] = copy[x2][y2], copy[x1][y1]
        return copy


def AllMoves(puz):
       
        moves = []
        i, j = IndexPosition(0,puz) 

        if i > 0:
            moves.append((swap(puz,i, j, i - 1, j)))  

        if j < COLUMNS - 1:
            moves.append((swap(puz,i, j, i, j + 1)))  

        if j > 0:
            moves.append((swap(puz,i, j, i, j - 1))) 

        if i < ROWS - 1:
            moves.append((swap(puz,i, j, i + 1, j)))

        return moves


def HDM(puz): #heuristic_manhattan_distance

        distance = 0
        for i in range(ROWS):
            for j in range(COLUMNS):
                i1, j1 = IndexPosition(puz[i][j], GOAL_PUZZLE)
                distance += abs(i - i1) + abs(j - j1)      
        return distance


def IndexPosition(data, puzzle):

        for i in range(ROWS):
            for j in range(COLUMNS):
                if puzzle[i][j] == data:
                    return i, j


def CNH(move, end_node): #calculate_new_heuristic
        return HDM(move) - HDM(end_node)


PUZZLE =list()
for i in range(4):
         a,b,c,d = map(int,input().split())
         PUZZLE.append([a,b,c,d])

ROWS = len(PUZZLE)
COLUMNS = len(PUZZLE[0])
GOAL_PUZZLE=[[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 0]]

if IsSolvable(PUZZLE):
    queue = [[HDM(PUZZLE), PUZZLE]]
    expanded = []
    path = None
    while queue:

            i = 0
            for j in range(1, len(queue)):
                if queue[i][0] > queue[j][0]:  
                    i = j
            path = queue[i]
            queue = queue[:i] + queue[i + 1:]
            end_node = path[-1]

            if end_node == GOAL_PUZZLE:
                break
            if end_node in expanded:
                continue

            for move in AllMoves(end_node):
                if move in expanded:
                    continue
                new_path = [path[0] + CNH(move, end_node)] + path[1:] + [move]
                queue.append(new_path)
                expanded.append(end_node)


    for k in range(1,len(path[1:])):
        for i in range(4):
            for j in range(4):
                if path[1:][k][i][j]!=path[1:][k-1][i][j] and path[1:][k][i][j]!=0:
                    print("move "+str(k)+": ",end='')
                    print("-> "+str(path[1:][k][i][j]))

    print("Number of movements performed : "+str(len(path[1:])-1))


else:
    print('This puzzle is not solvable')


    
    
