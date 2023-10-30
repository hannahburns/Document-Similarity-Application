# Document Similarity Command-Line Application

## Introduction

This project is an implementation of a command-line application in OCaml that calculates document similarity without using explicit recursion or looping. Document similarity is a crucial concept in various "big data" applications, such as improving search, language recognition, automated document classification, automated document summary, authorship attribution, and plagiarism detection. The application compares a target document to a list of representative documents and determines the most similar document from the list. It then reports the most similar document and its similarity score.

## Getting Started

To run the application, compile the application using the following command:

   ```
   ocamlopt -o findsim fTools.ml similar.ml findsim.ml
   ```

3. Run the application by providing the name of the file listing the representative documents and the name of the target document as command-line arguments:

   ```
   ./findsim [options] repfile_list target_name
   ```

   - `[options]` can be `--all` or empty. If `--all` is provided, the application will display similarity scores for all representative documents. Otherwise, it will only show the most similar document.
   - `repfile_list` is the name of the file containing a list of representative document filenames.
   - `target_name` is the name of the target document.

## Implementation Details

### Task 1: Reading the File List

The application reads the list of representative files from the file specified as the first command-line argument. It uses the `file_lines` function from `fTools.ml` to read the file and store the list of file names.

### Task 2: Reading the Representative Files and the Document

The application uses the `file_as_string` function from `fTools.ml` to read the contents of both the target and representative files. It stores the target file's content in `target_contents` and the contents of all representative files in `rep_contents`.

### Task 3: Splitting into N-Grams

The application extracts normalized n-grams (3-grams) from the text using the `n_grams` function. This function preprocesses the text by converting it to lowercase, removing non-alphabetic characters, and extracting n-grams. The resulting n-grams are stored in `target_ngrams` for the target document and `rep_ngrams` for the representative documents.

### Task 4: Converting to Multisets

The application represents each document as a multiset of n-grams using associative lists. The function `multiset_of_list` converts a list of n-grams into a multiset. It ensures that each n-gram is associated with its multiplicity. The representative documents are converted into a list of multisets in `rep_multisets`, and the target document is converted into a multiset in `target_multiset`.

### Task 5: Define the Similarity Function

The similarity between two documents is defined as the ratio of the size of the intersection of their n-gram multisets to the size of the union. The application defines functions for calculating the intersection size, union size, and similarity. These functions use List functions to work with multisets represented as associative lists.

### Task 6: Compute the Closest Document

The application computes the most similar representative document to the target document and its similarity score using the `find_max` function. It finds the representative document with the highest similarity score and returns its name and score. In case of multiple documents with the same similarity score, it selects the lexicographically greatest document name.

### Task 7: Print Out the Result(s)

The application prints the results based on the provided options. If `--all` is specified, it prints similarity scores for all representative documents. Otherwise, it only shows the most similar document and its similarity score.

## Testing

The application can be tested using the provided representative and target files. By running the application with different target files, you can observe the similarity scores and determine which representative document is most similar.

## Conclusion

This command-line application efficiently calculates document similarity without explicit recursion or looping. It is suitable for a wide range of applications, from content recommendation systems to plagiarism detection. The implementation is both functional and efficient, and it follows best practices for OCaml programming.
