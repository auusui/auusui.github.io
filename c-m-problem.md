;;; format of state (#C #M W/E)
;;; start is all on west (3 3 W)
;;; goal is all on east (0 0 E)
;;; I had help coding from Professor Binstead, comments are mine

; constants are set as stated above, moves has the move function names
(defconstant *start* '(3 3 W))
(defconstant *goal* '(0 0 E))
(defconstant *moves* '(C1 C2 C1M1 M1 M2))


;; function that will check if state is valid
;; cases: if M=0, if M >= C, if C > M, If it goes below 0 or above 3 for each
;; returns NIL on false and the state on true
(defun is-valid (state)
  (cond
   ; checks if C is more than 3
   ((> (nth 0 state) 3) nil) 
   ; checks if C is less than 0
   ((< (nth 0 state) 0) nil) 
   ; checks if M is more than 3
   ((> (nth 1 state) 3) nil) 
   ; checks if M is less than 0
   ((< (nth 1 state) 0) nil) 
   ; checks if there are more cannibals than missionaries while M > 0
   ((and (> (nth 0 state) (nth 1 state)) (> (nth 1 state) 0)) nil) 
   ; subtracts 3 from both sides if C > M and 3 > M
   ((and (> (- 3 (nth 0 state)) (- 3 (nth 1 state))) (> 3 (nth 1 state))) nil) 
   ; state passes tests and is returned to be listed
   (t (list state))))

; moves 1 cannibal across the stream
(defun C1 (state)
  (cond
   ; if the boat is on the west, we move C to the east
   ((equal (nth 2 state) 'w) (is-valid (list (- (nth 0 state) 1) (nth 1 state) 'e))) 
   ; else we move C to the west
   (t (is-valid (list (+ (nth 0 state) 1) (nth 1 state) 'w))))) 


; moves 2 cannibals across the stream
(defun C2 (state)
  (cond
   ; if boat on west, move 2 C's to the east
   ((equal (nth 2 state) 'w) (is-valid (list (- (nth 0 state) 2) (nth 1 state) 'e))) 
   ; else move 2 C's west
   (t (is-valid (list (+ (nth 0 state) 2) (nth 1 state) 'w))))) 


; moves 1 cannibal and 1 missionary across stream
(defun C1M1 (state)
  (cond
   ; if boat on west, move them to east
   ((equal (nth 2 state) 'w) (is-valid (list (- (nth 0 state) 1) (- (nth 1 state) 1) 'e))) 
   ; else move them west
   (t (is-valid (list (+ (nth 0 state) 1) (+ (nth 1 state) 1) 'w))))) 


; moves 1 missionary across stream
(defun M1 (state)
  (cond
   ; if boat on west, move M to east
   ((equal (nth 2 state) 'w) (is-valid (list (nth 0 state) (- (nth 1 state) 1) 'e))) 
   ; else move to west
   (t (is-valid (list (nth 0 state) (+ (nth 1 state) 1) 'w))))) 


; moves 2 missionaries across stream
(defun M2 (state)
  (cond
   ; if boat on west, move 2 M's to east
   ((equal (nth 2 state) 'w) (is-valid (list (nth 0 state) (- (nth 1 state) 2) 'e)))
   ; else move them to west
   (t (is-valid (list (nth 0 state) (+ (nth 1 state) 2) 'w))))) 


;; functon that will find the h(s) value and return the h(s) value
; it should be all 0, do nth 0/1 state - 0, if > 0, add up amount of differences for both positions = h(s) value

(defun find-h (state)
  (+ (nth 0 state) (nth 1 state)))
