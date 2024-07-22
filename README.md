class State:
    def __init__(self,jug1,jug2):
        self.jug1=jug1
        self.jug2=jug2
    def __eq__(self,other):
        return self.jug1 == other.jug1 and self.jug2 == other.jug2
    def __hash__(self):
        return hash((self.jug1,self.jug2))
    def __str__(self):
        return f"({self.jug1},{self.jug2})"
    
class Node:
    def __init__(self,state,parent=None):
        self.state=state
        self.parent=parent
    def path(self):
        if self.parent is None:
            return [self.state]
        else:
            return self.parent.path()+[self.state]
        
    def dfs(start_state,goal):
        visited=set()
        stack=[Node(start_state)]
        while stack:
            node=stack.pop()
            state=node.state
            if state == goal:
                return node.path()
            visited.add(state)
            actions=[
                (state.jug1,4),
                (4,state.jug2),
                (0,state.jug2),
                (state.jug1,0),
                (min(state.jug1+state.jug2,4),max(0,state.jug1+state.jug2-4)),
                (max(0,state.jug1+state.jug2-3),min(state.jug1+state.jug2,3))
            ]
            for action in actions:
                new_state = State(action[0],action[1])
                if new_state not in visited:
                    stack.append (Node(new_state,node))
        return none
        
start_state = State(0,0)
goal_state = State(2,0)
print("Starting DFS for water jug problem...")
path = Node.dfs(start_state, goal_state)
if path:
    print("Solution found! steps to reach the goal:")
    for i, state in enumerate(path):
        print(f"step{i}:jug1:{state.jug1},jug2:{state.jug2}")
else:
         print("No solution found!")
