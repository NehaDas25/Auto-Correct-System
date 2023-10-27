# Work Report

## Information

- Name: <ins> DAS, NEHA </ins>
- GitHub: <ins> NehaDas25 </ins>



## Features

- Not Implemented:
  - Nothing

<br><br>

- Implemented:In this project, to achieve the end goal, all parts are implemented sequentially.
  - PART 1: DATA PREPROCESSING
     - Exercise 1: process_data
       - Implemented the function process_data() with the input file_name.
       - In this function we have to open the file, read its contents into a string variable.
       - Change everything to lower case.
       - Store the list of words using "words = re.findall(r'\w+', read_file_name)".
       - Tested the function using "shakespeare.txt".
       - This passed all the unit-test cases.

     - Exsercise 2: get_count
       - Implemented a get_count() function with input word_l.
       - This function returns a dictionary where the key is a word and the value is the number of times the word appears in the list and is stored word_count_dict.
       - This passed all the unit-test cases as well.

     - Exercise 3: get_probs
       - Implemented get_probs() function with input word_count_dict.
       - This returns the probability that a word occurs in a sample.
       - It returns a dictionary where the keys are words, and the value for each word is its probability in the corpus of words and is stored under a variable probs that is "probs[key] = word_count_dict[key]/M". 
       - This passed all the unit-test cases as well.

  - PART 2: STRING MANIPULATION - In this, four function has been implemented amd list comprehensions has been used.
     - Exercise 4 - delete_letter
       - Implemented a delete_letter() function with inputs word, verbose=False.
       - This function returns a list of strings with one character deleted. For this we have to follow to two steps.
       - In the Step 1, a splits list has been created using list comprehension and is stored under "split_l = [(word[:i],word[i:]) for i in range(len(word)+1)]".
       - In the Step 2, is to delete_letter. Here, we are generating all words that result from deleting one character.This can be done in a single line with a list comprehension that is stored under **delete_l = [(L+R[1:]) for L,R in split_l if R]**.
       - For testing we have taken the word = "cans", So the output is: 
        split_l = [('', 'cans'), ('c', 'ans'), ('ca', 'ns'), ('can', 's'), ('cans', '')]
        delete_l = ['ans', 'cns', 'cas', 'can'].
       - This passed all the unit-test cases as well.

     - Exercise 5 -  switch_letter
       - Implemented a  switch_letter() function with inputs word, verbose=False.
       - This function returns a list of all the possible switches of two letters that are **adjacent to each other**.
       - In the Step 1, a splits list has been created using list comprehension and is stored under **split_l = [(word[:i],word[i:]) for i in range(len(word)+1)]**.
       - In the Step 2, A list comprehension has been used which forms strings by swapping adjacent letters. Here 'condition' will test the length of R in a given iteration and is stored under **switch_l = [L+R[1]+R[0]+R[2:] for L,R in split_l if len(R)>=2]**.
       - For testing we have taken the word = "eta", So the output is: 
       split_l = [('', 'eta'), ('e', 'ta'), ('et', 'a'), ('eta', '')] 
       switch_l = ['tea', 'eat'].
       - This passed all the unit-test cases as well.  

     - Exercise 6 -  replace_letter
       - Implemented a  replace_letter() function with inputs word, verbose=False.
       - This function returns a list of strings with one replaced letter from the original word.
       - In the Step 1, a splits list has been created using list comprehension and is stored under **split_l = [(word[:i],word[i:]) for i in range(len(word)+1)]**.
       - In the Step 2, A list comprehension which form strings by replacing letters.The use of the second for loop.It is expected in this routine that one or more of the replacements will include the original word and is stored under **replace_l=[L+i+(R[1:] if len(R)>1 else '') for L,R in split_l if R for i in letters]**.
       - In Step 3, removed the original input letter from the output.
       - This passed all the unit-test cases as well.

     - Exercise 7 - insert_letter
       - Implemented a insert_letter() function with inputs word, verbose=False.
       - This function  returns a list with a letter inserted at every offset.
       - In the Step 1, a splits list has been created using list comprehension and is stored under **split_l = [(word[:i],word[i:]) for i in range(len(word)+1)]**.
       - In the Step 2, A list comprehension which form strings by inserting letters and is stored under **insert_l=[L+i+R for L,R in split_l for i in letters]**.
       - This passed all the unit-test cases as well.

   - PART 3: Combining the Edits
   - PART 3.1: Edit One Letter
     - Exercise 8: edit_one_letter
       - Implemented the edit_one_letter() function with the inputs word, allow_switches = True.
       - This function helps us to find all the possible edits that are one edit away from a word and this consist of the replace, insert, delete, and optionally the switch operation.
       - Used previously implemented function that are delete_letter(), replace_letter(), insert_letter() and switch_letter()(optionally).
       - These functions return lists while edit_one_letter() function should return a python set. 
       - This passed all the unit-test cases as well.

   - PART 3.2: edit_two_letters  
     - Exercise 9: edit_two_letters
       - Implemented the edit_two_letters() function with the inputs word, allow_switches = True.
       - Here, we have to get all the possible edits on a single word and then for each modified word, we have to modify it again.
       - Here, two loops has been used. First loop will be used to find the single edits using edit_one_letter() and second loop will all the edits based on the first loop results.
       - This passed all the unit-test cases as well.

   - PART 3.3: Suggest Spelling Suggestions
     - Exercise 10: get_corrections
       - Implemented get_corrections() function with the inputs word, probs, vocab, n=2, verbose = False.
       - This functionreturns a list of zero to n possible suggestion tuples of the form (word, probability_of_word). There are 3 steps to follow.
       - In **Step 1**,Generated suggestions for a supplied word, with the previous edit functions. This suggestion algorithm has logics to follow:
          1. If the word is in the vocabulary, suggest the word.
          2. Otherwise, if there are suggestions from edit_one_letter that are in the vocabulary, use those.
          3. Otherwise, if there are suggestions from edit_two_letters that are in the vocabulary, use those.
          4. Otherwise, suggest the input word.
          5. The idea is that words generated from fewer edits are more likely than words with more edits.
       - Here the suggesstions are created using *short-circuit behaviour*. 
       - In **Step 2**,Created a 'best_words' dictionary where the 'key' is a suggestion and the 'value' is the probability of that word in your vocabulary. If the word is not in the vocabulary, assign it a probability of 0.
       - In **Step 3**, Selected the n best suggestions. There may be fewer than n.
       - This passed all the unit-test cases as well.
       
   - PART 4: Minimum Edit Distance
   - PART 4.1: Dynamic Programming
     - Exercise 11: min_edit_distance 
       - Implemented the function min_edit_distance() with the inputs used are source, target, ins_cost = 1, del_cost = 1, rep_cost = 2.
       - source: a string corresponding to the string you are starting with.
       - target: a string corresponding to the string you want to end with.
       - Used deletion(del_cost) and insert cost(ins_cost) as 1.
       - Initialize cost matrix with zeros and dimensions (m+1,n+1), here *m = len(source) and n = len(target)*.
       - Filled in column 0, from row 1 to row m, both inclusive that is  **D[row,0] = D[row-1,0]+del_cost**.
       - Filled in row 0, for all columns from 1 to n, both inclusive that is **D[0,col] = D[0,col-1]+ins_cost**.
       - Looped through row 1 to row m as well as through column 1 to column n,(both inclusive) with r_cost intialized to rep_cost. 
       - Checked to see if source character at the previous row matches the target character at the previous column, then update **r_cost to 0** otherwise update **D[row,col] = min(D[row-1,col]+del_cost, D[row,col-1]+ins_cost, D[row-1,col-1]+r_cost)**.
       - Lastly find minimum edit distance with the cost found at row m, column n.
       - This passed all the unit-test cases as well.


      

    
<br><br>

- Partly implemented:
  - w1_unittest.py was not implemented as part of assignment to pass all unit-tests for the graded functions(). It was already created by the Professor.

<br><br>

- Bugs
  - No bugs

<br><br>


## Reflections

- Assignment is very good, but little bit of difficulty. Gives a thorough understanding of the basis of Autocorrect with its edits function, Dynamic Programming.


## Output

### output:

<pre>
<br/><br/>
Out[3] - 
  The first ten words in the text are: 
  ['o', 'for', 'a', 'muse', 'of', 'fire', 'that', 'would', 'ascend', 'the']
  There are 6116 unique words in the vocabulary.
   
   Expected Output
    The first ten words in the text are: 
    ['o', 'for', 'a', 'muse', 'of', 'fire', 'that', 'would', 'ascend', 'the']
    There are 6116 unique words in the vocabulary.

 Out[4] - All tests passed

 Out[6] - 
  There are 6116 key values pairs
  The count for the word 'thee' is 240
   Expected Output
    There are 6116 key values pairs
    The count for the word 'thee' is 240

 Out[7] -  All tests passed 

 Out[9] - Length of probs is 6116
 P('thee') is 0.0045

  Expected output:
      Length of probs is 6116
      P('thee') is 0.0045
 
 Out[10] -  All tests passed
 Out[12] -
 input word cans, 
 split_l = [('', 'cans'), ('c', 'ans'), ('ca', 'ns'), ('can', 's'), ('cans', '')], 
 delete_l = ['ans', 'cns', 'cas', 'can']
 
  Expected Output:
      Note: You might get a slightly different result with split_l
      input word cans, 
      split_l = [('', 'cans'), ('c', 'ans'), ('ca', 'ns'), ('can', 's')], 
      delete_l = ['ans', 'cns', 'cas', 'can']

 Out[13] - Number of outputs of delete_letter('at') is 2
  
  Expected output
     Number of outputs of delete_letter('at') is 2

 Out[14] -  All tests passed
 
 Out[16] -
 Input word = eta 
 split_l = [('', 'eta'), ('e', 'ta'), ('et', 'a'), ('eta', '')] 
 switch_l = ['tea', 'eat']
 
  Expected Output:
      Note: You might get a slightly different result with split_l
      Input word = eta 
      split_l = [('', 'eta'), ('e', 'ta'), ('et', 'a')] 
      switch_l = ['tea', 'eat']

 Out[17] - Number of outputs of switch_letter('at') is 1
  
 Expected output
      Number of outputs of switch_letter('at') is 1

 Out[18] - All tests passed

 Out[16] -
 Input word = can 
 split_l = [('', 'can'), ('c', 'an'), ('ca', 'n'), ('can', '')] 
 replace_l ['aan', 'ban', 'caa', 'cab', 'cac', 'cad', 'cae', 'caf', 'cag', 'cah', 'cai', 'caj', 'cak', 'cal', 'cam', 'cao', 'cap', 'caq', 'car', 'cas', 'cat', 'cau', 'cav', 'caw', 'cax', 'cay', 'caz', 'cbn', 'ccn', 'cdn', 'cen', 'cfn', 'cgn', 'chn', 'cin', 'cjn', 'ckn', 'cln', 'cmn', 'cnn', 'con', 'cpn', 'cqn', 'crn', 'csn', 'ctn', 'cun', 'cvn', 'cwn', 'cxn', 'cyn', 'czn', 'dan', 'ean', 'fan', 'gan', 'han', 'ian', 'jan', 'kan', 'lan', 'man', 'nan', 'oan', 'pan', 'qan', 'ran', 'san', 'tan', 'uan', 'van', 'wan', 'xan', 'yan', 'zan']
 
  Expected Output:
      Input word = can 
      split_l = [('', 'can'), ('c', 'an'), ('ca', 'n')] 
      replace_l ['aan', 'ban', 'caa', 'cab', 'cac', 'cad', 'cae', 'caf', 'cag', 'cah', 'cai', 'caj', 'cak', 'cal', 'cam', 'cao', 'cap', 'caq', 'car', 'cas', 'cat', 'cau', 'cav', 'caw', 'cax', 'cay', 'caz', 'cbn', 'ccn', 'cdn', 'cen', 'cfn', 'cgn', 'chn', 'cin', 'cjn', 'ckn', 'cln', 'cmn', 'cnn', 'con', 'cpn', 'cqn', 'crn', 'csn', 'ctn', 'cun', 'cvn', 'cwn', 'cxn', 'cyn', 'czn', 'dan', 'ean', 'fan', 'gan', 'han', 'ian', 'jan', 'kan', 'lan', 'man', 'nan', 'oan', 'pan', 'qan', 'ran', 'san', 'tan', 'uan', 'van', 'wan', 'xan', 'yan', 'zan']

 Out[21] - Number of outputs of replace_letter('at') is 50
  
 Expected output
      Number of outputs of replace_letter('at') is 50

 Out[22] - All tests passed

 Out[24] -
 Input word at 
 split_l = [('', 'at'), ('a', 't'), ('at', '')] 
 insert_l = ['aat', 'bat', 'cat', 'dat', 'eat', 'fat', 'gat', 'hat', 'iat', 'jat', 'kat', 'lat', 'mat', 'nat', 'oat', 'pat', 'qat', 'rat', 'sat', 'tat', 'uat', 'vat', 'wat', 'xat', 'yat', 'zat', 'aat', 'abt', 'act', 'adt', 'aet', 'aft', 'agt', 'aht', 'ait', 'ajt', 'akt', 'alt', 'amt', 'ant', 'aot', 'apt', 'aqt', 'art', 'ast', 'att', 'aut', 'avt', 'awt', 'axt', 'ayt', 'azt', 'ata', 'atb', 'atc', 'atd', 'ate', 'atf', 'atg', 'ath', 'ati', 'atj', 'atk', 'atl', 'atm', 'atn', 'ato', 'atp', 'atq', 'atr', 'ats', 'att', 'atu', 'atv', 'atw', 'atx', 'aty', 'atz']
 Number of strings output by insert_letter('at') is 78
 
  Expected Output:
      Input word at 
      split_l = [('', 'at'), ('a', 't'), ('at', '')] 
      insert_l = ['aat', 'bat', 'cat', 'dat', 'eat', 'fat', 'gat', 'hat', 'iat', 'jat', 'kat', 'lat', 'mat', 'nat', 'oat', 'pat', 'qat', 'rat', 'sat', 'tat', 'uat', 'vat', 'wat', 'xat', 'yat', 'zat', 'aat', 'abt', 'act', 'adt', 'aet', 'aft', 'agt', 'aht', 'ait', 'ajt', 'akt', 'alt', 'amt', 'ant', 'aot', 'apt', 'aqt', 'art', 'ast', 'att', 'aut', 'avt', 'awt', 'axt', 'ayt', 'azt', 'ata', 'atb', 'atc', 'atd', 'ate', 'atf', 'atg', 'ath', 'ati', 'atj', 'atk', 'atl', 'atm', 'atn', 'ato', 'atp', 'atq', 'atr', 'ats', 'att', 'atu', 'atv', 'atw', 'atx', 'aty', 'atz']
      Number of strings output by insert_letter('at') is 78

 Out[25] - All tests passed

 Out[29] -
 input word at 
 edit_one_l 
 ['a', 'aa', 'aat', 'ab', 'abt', 'ac', 'act', 'ad', 'adt', 'ae', 'aet', 'af', 'aft', 'ag', 'agt', 'ah', 'aht', 'ai', 'ait', 'aj', 'ajt', 'ak', 'akt', 'al', 'alt', 'am', 'amt', 'an', 'ant', 'ao', 'aot', 'ap', 'apt', 'aq', 'aqt', 'ar', 'art', 'as', 'ast', 'ata', 'atb', 'atc', 'atd', 'ate', 'atf', 'atg', 'ath', 'ati', 'atj', 'atk', 'atl', 'atm', 'atn', 'ato', 'atp', 'atq', 'atr', 'ats', 'att', 'atu', 'atv', 'atw', 'atx', 'aty', 'atz', 'au', 'aut', 'av', 'avt', 'aw', 'awt', 'ax', 'axt', 'ay', 'ayt', 'az', 'azt', 'bat', 'bt', 'cat', 'ct', 'dat', 'dt', 'eat', 'et', 'fat', 'ft', 'gat', 'gt', 'hat', 'ht', 'iat', 'it', 'jat', 'jt', 'kat', 'kt', 'lat', 'lt', 'mat', 'mt', 'nat', 'nt', 'oat', 'ot', 'pat', 'pt', 'qat', 'qt', 'rat', 'rt', 'sat', 'st', 't', 'ta', 'tat', 'tt', 'uat', 'ut', 'vat', 'vt', 'wat', 'wt', 'xat', 'xt', 'yat', 'yt', 'zat', 'zt']

 The type of the returned object should be a set <class 'set'>
 Number of outputs from edit_one_letter('at') is 129
 
  Expected Output:
      input word at 
      edit_one_l 
      ['a', 'aa', 'aat', 'ab', 'abt', 'ac', 'act', 'ad', 'adt', 'ae', 'aet', 'af', 'aft', 'ag', 'agt', 'ah', 'aht', 'ai', 'ait', 'aj', 'ajt', 'ak', 'akt', 'al', 'alt', 'am', 'amt', 'an', 'ant', 'ao', 'aot', 'ap', 'apt', 'aq', 'aqt', 'ar', 'art', 'as', 'ast', 'ata', 'atb', 'atc', 'atd', 'ate', 'atf', 'atg', 'ath', 'ati', 'atj', 'atk', 'atl', 'atm', 'atn', 'ato', 'atp', 'atq', 'atr', 'ats', 'att', 'atu', 'atv', 'atw', 'atx', 'aty', 'atz', 'au', 'aut', 'av', 'avt', 'aw', 'awt', 'ax', 'axt', 'ay', 'ayt', 'az', 'azt', 'bat', 'bt', 'cat', 'ct', 'dat', 'dt', 'eat', 'et', 'fat', 'ft', 'gat', 'gt', 'hat', 'ht', 'iat', 'it', 'jat', 'jt', 'kat', 'kt', 'lat', 'lt', 'mat', 'mt', 'nat', 'nt', 'oat', 'ot', 'pat', 'pt', 'qat', 'qt', 'rat', 'rt', 'sat', 'st', 't', 'ta', 'tat', 'tt', 'uat', 'ut', 'vat', 'vt', 'wat', 'wt', 'xat', 'xt', 'yat', 'yt', 'zat', 'zt']

      The type of the returned object should be a set <class 'set'>
      Number of outputs from edit_one_letter('at') is 129

 Out[30] - All tests passed

 Out[34] -
 Number of strings with edit distance of two: 2654
 First 10 strings ['', 'a', 'aa', 'aaa', 'aab', 'aac', 'aad', 'aae', 'aaf', 'aag']
 Last 10 strings ['zv', 'zva', 'zw', 'zwa', 'zx', 'zxa', 'zy', 'zya', 'zz', 'zza']
 The data type of the returned object should be a set <class 'set'>
 Number of strings that are 2 edit distances from 'at' is 7154
 
  Expected Output:
      Number of strings with edit distance of two: 2654
      First 10 strings ['', 'a', 'aa', 'aaa', 'aab', 'aac', 'aad', 'aae', 'aaf', 'aag']
      Last 10 strings ['zv', 'zva', 'zw', 'zwa', 'zx', 'zxa', 'zy', 'zya', 'zz', 'zza']
      The data type of the returned object should be a set <class 'set'>
      Number of strings that are 2 edit distances from 'at' is 7154

 Out[35] - All tests passed

 Out[201] -
 entered word =  dys 
suggestions =  ['days', 'dye']
 word 0: days, probability 0.000410
 word 1: dye, probability 0.000019
 data type of corrections <class 'list'>
 
  Expected Output:
      Note: This expected output is for my_word = 'dys'. Also, keep verbose=True
      entered word =  dys 
      suggestions =  {'days', 'dye'}
      word 0: days, probability 0.000410
      word 1: dye, probability 0.000019
      data type of corrections <class 'list'>

 Out[202] - All tests passed

 Out[195] -
 minimum edits:  4 

    #  s  t  a  y
 #  0  1  2  3  4
 p  1  2  3  4  5
 l  2  3  4  5  6
 a  3  4  5  4  5
 y  4  5  6  5  4

  Expected Output:
      minimum edits:  4

      #  s  t  a  y
   #  0  1  2  3  4
   p  1  2  3  4  5
   l  2  3  4  5  6
   a  3  4  5  4  5
   y  4  5  6  5  4

Out[196] -
 minimum edits:  3 

    #  n  e  a  r
 #  0  1  2  3  4
 e  1  2  1  2  3
 e  2  3  2  3  4
 r  3  4  3  4  3

  Expected Output:
      minimum edits:  3 

     #  n  e  a  r
  #  0  1  2  3  4
  e  1  2  1  2  3
  e  2  3  2  3  4
  r  3  4  3  4  3

Out[197] - All tests passed

Out[198] - (empty)

  Expected Results

     (empty)

Out[199] - 
 eer eer 0
  
  Expected Results

     eer eer 0




<br/><br/>
</pre>
