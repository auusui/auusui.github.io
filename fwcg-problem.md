;;; start is going to be all of them on the west side (1 1 1 1)
;;; goal is all of them on the east side (0 0 0 0)
;;; order of permutation is (farmer, wolf, cabbage, goat)
;;; in all functions, farmer is default opposite every move because he takes himself with one of the others every trip across
;; I had help with functions through "http://www2.hawaii.edu/~chin/361/Class/fwgc.lisp" I used the safe function and implemented the opposite function for cleaner code



; constants are set as stated above, moves has the move function names
(defconstant *start* '(1 1 1 1))
(defconstant *goal* '(0 0 0 0))
(defconstant *moves* '(farmer-takes-wolf farmer-takes-goat farmer-takes-cabbage farmer-takes-self))


;; functions that tell what side each is on

(defun farmer-side (state)
  (nth 0 state))

(defun wolf-side (state)
  (nth 1 state))

(defun cabbage-side (state)
  (nth 2 state))

(defun goat-side (state)
  (nth 3 state))


;; checks to see if the state is valid
;; cases: if W & G alone, if G & C alone

(defun is-valid (state)
  (cond 
   ; if goat and cabbage are on the same side while farmer is on the other side, return nil
   ((and (eq (goat-side state) (cabbage-side state))
         (not (eq (farmer-side state) (goat-side state))))
    nil)
   ; if goat and wolf are on the same side while farmer is on the other side, return nil
   ((and (eq (goat-side state) (wolf-side state))
         (not (eq (farmer-side state) (goat-side state))))
    nil)
   (t state)))



;; given the original side, it returns the opposite side
; east = 0, west = 1
(defun opposite (side)
  (cond 
   ; if it is on the east, switch to the west
   ((eq side 0) 1)
   ; if it is on the west, swith to the east
   ((eq side 1) 0)
   (t (print "error in opposite, side is not e or w"))))



;; takes the farmer himself to the other side
(defun farmer-takes-self (state)
  ; check if state is valid
  ; calls on opposite of only farmer side
  (is-valid (list (opposite (farmer-side state))
                  (wolf-side state)
                  (cabbage-side state)
                  (goat-side state))))



;; takes the wolf to the other side
(defun farmer-takes-wolf (state)
  (cond 
   ; checks if the farmer and wolf are on the same side to begin with
   ((eq (farmer-side state) (wolf-side state))
        ; checks if state is valid, switches side for farmer and wolf   
        (is-valid (list (opposite (farmer-side state))
                        (opposite (wolf-side state))
                        (cabbage-side state)
                        (goat-side state))))
   ; else farmer cannot take wolf if wolf is on the other side
   (t nil)))



;; takes the goat to the other side
(defun farmer-takes-goat (state)
  (cond 
   ; checks if the farmer and goat are on the same side to begin with
   ((eq (farmer-side state) (goat-side state))
    ; checks state is valid, swtiches side of farmer and goat
    (is-valid (list (opposite (farmer-side state))
                    (wolf-side state)
                    (cabbage-side state)
                    (opposite (goat-side state)))))
        ; else farmer cannot take goat if goat is on the other side
        (t nil)))



;; takes the cabbage to the other side
(defun farmer-takes-cabbage (state)
  (cond 
   ; checks if the farmer and cabbage are on the same side to begin with
   ((eq (farmer-side state) (cabbage-side state))
    ; checks state is valid, switches side of farmer and cabbage
    (is-valid (list (opposite (farmer-side state))
                    (wolf-side state)
                    (opposite (cabbage-side state))
                    (goat-side state))))
        ; else farmer cannot take cabbage if cabbage is on the other side
        (t nil)))



;; functon that will find the h(s) value
; there should be all 0 (east), each one that is a 1 (west) = +1 to h(s) value

(defun find-h (state)
  (+ (+ (nth 0 state) (nth 1 state)) (+ (nth 2 state) (+ nth 3 state))))







