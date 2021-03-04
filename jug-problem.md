;;; start is all of the jugs empty (0 0)
;;; goal is the 5G with 4 gallons of water (4 0)
;;; order of the permutations is (5-gallon 3-gallon)


; constants are set as stated above, moves has the move function names
(defconstant *start* '(0 0))
(defconstant *goal* '(4 0))
(defconstant *moves* '(fill5G 3F5-to3 fill2-5G empty3 2F5-to3 1F5-to3))


;; function that will check if state is valid
;; cases: if 5G is between 0-5 gallons full, if 3G is btwn 0-3 gallons full
;; returns NIL on false and the state on true
(defun fill-check (state)
  (cond
   ; if 5G is more than 5 gals , if 3G is more than 3 gals, return nil
   ((> (nth 0 state) 5) nil)
   ((> (nth 1 state) 3) nil)
   ; if 5G is less than 0 gals , if 3G is less than 0 gals, return nil
   ((< (nth 0 state) 0) nil)
   ((< (nth 1 state) 0) nil)
   (t (list state))))



;; functions that will add or subtract gallons from the 2 jugs

;;; empties 1 gallon from 5G to 3G
(defun 1F5-to3 (state)
  (cond
   (t (fill-check (list (- (nth 0 state) 1) (+ (nth 1 state) 1) )))))


;;; empties 2 gallons from 5G to 3G
(defun 2F5-to3 (state)
  (cond
   (t (fill-check (list (- (nth 0 state) 2) (+ (nth 1 state) 2) )))))


;;; empties 3 gallons from 5G to 3G
(defun 3F5-to3 (state)
  (cond
  (t (fill-check (list (- (nth 0 state) 3) (+ (nth 1 state) 3) )))))


;;; Add 2 gallons to 5G
(defun fill2-5G (state)
  (cond 
  (t (fill-check (list (+ (nth 0 state) 2) (nth 1 state) )))))


;;; add 5 gallons to 5G
(defun fill5G (state)
  (cond
   (t (fill-check (list (+ (nth 0 state) 5) (nth 1 state) )))))


;;; empty 3G
(defun empty3 (state)
  (cond 
  (t (fill-check (list (nth 0 state) 0)))))




;; functon that will find the h(s) value
; there should be all E, each one that is a W = +1 to h(s) value

(defun find-h (state)
  (abs (- 4 (nth 0 state))))




