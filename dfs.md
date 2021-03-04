; start is the state that we will start at for each situation
; goal is the state that we want to end with at the end 
; open is a list of the states that aren't explored yet
; closed is a list of the states used 
; each move is going to be a cost of 1.  The g(s) will be the same for each move therefore making the g(s) for the whole path, the length of the closed list for each iteration
; I had help on this code from Professor Binstead for Assignment 2, the comments are mine and the code is hers


;; runs the dfs function with the start, goal, and moves
;; main function
(defun run-dfs (start goal moves)
  (dfs (list (list start nil)) nil goal moves)) 

;; function definition for the depth-first-search 
;; keeps checking if the goal is met or not, if not met, calls another move
(defun dfs (open closed goal moves)
  ; print first node of open list each iteration
  (format t "Open list: ~A.~%" open)
  (cond
   ; if the list is empty, return nil
   ((null open) (format t "Open list is empty.~%") nil) 
   ; if the goal and state is the same, then the goal was found, then prints solution, length of both lists, and path
   ((equal (first (first open)) goal) (format t "Found goal: ~A.~% Solution path: ~A.~% Length of open list: ~A.~% Length of closed list: ~A.~%" goal (reverse (cons goal (nth 1 (first open)))) (length open) (length closed)) t) 
   ; call mymember function, if true -- call dfs on rest of open list (without first node) because it is already done
   ((mymember (first (first open)) closed) (dfs (rest open) closed goal moves)) 
   ; call dfs, use order-list function to order the children from least to greatest f(s) value and insert into open list
   (t (dfs (order-list (generate-children (first open) moves) (rest open)) (cons (first (first open)) closed) goal moves)))) 

; function that checks if the two nodes are a member in the open and closed list
(defun mymember (item list)
  (cond
   ; list is null, return nil
   ((null list) nil)
   ; if the two items are equal, return true
   ((equal item (first list)) t)
   ; else recursively call function with list minus the first node in list
   (t (mymember item (rest list)))))

;; This function will generate the "children" for each call for a state
(defun generate-children (node moves)
  (cond
   ; no moves left, return nil
   ((null moves) nil)
   
   ; plucks out the null moves
   ((null (funcall (first moves) (first node))) (generate-children node (rest moves)))
   
   ; adding state to node list path
   ; recursively call generate-children to get more successors
   (t (cons
       (list (first (funcall (first moves) (first node))) (cons (first node) (nth 1 node))) 
       (generate-children node (rest moves))))))


; gets the f-value
(defun heuristic-search (node)
  (cond
   ; if there is nothing in the node list, return nil
   ((null (first node)) nil)
   (t (+ (find-h (first node)) (length (car (cdr node)))))))


; inserts the item in the correct order 
(defun place-item (state li) 
  (cond
   ; if the list is null, num is the only child
   ((null li) (list state))
   ; if num is the least, add to the front of list
   ((<= (heuristic-search state) (heuristic-search (first li))) (cons state li))
   ; else move on to the next spot
   (t (cons (first li) (place-item state (rest li))))
   ))

; restructures the open list to the correct order
; list1 is the list with the children nodes from generate-children
; list2 is the open list we already have
(defun order-list (list1 list2) 
  (cond
   ((null list1) list2)
   (t (place-item (first list1) (order-list (rest list1) list2)))
   ))

