### EX5 Information Retrieval Using Boolean Model in Python
### DATE: 14/02/2026
### AIM: To implement Information Retrieval Using Boolean Model in Python.
### Description:
<div align = "justify">
The Boolean model in Information Retrieval (IR) is a fundamental model used for searching and retrieving information from a collection of documents. It operates on the principles of set theory and logic, where documents are represented as sets of terms or words, and queries are expressed as Boolean expressions using logical operators such as AND, OR, and NOT.
  
### Procedure:
1. ***Initialize the BooleanRetrieval class:*** The BooleanRetrieval class is defined to manage the indexing and searching of documents.
2. ***Constructor and Index Initialization:*** The class constructor initializes an empty index to store the inverted index mapping terms to documents.
3. ***Indexing Documents:***
    <p> a) The index_document method is responsible for indexing documents.
    <p> b) Tokenize the text content of documents, converting them into lowercase terms.
    <p> c) For each term in the document, it adds an entry in the index, associating the term with the document ID. </p>
4. ***Fetch Web Page Text:***
    <p>a) The fetch_webpage_text method uses the requests library to fetch content from a given URL.
    <p>b) Extract text content from the fetched HTML using BeautifulSoup.
    <p>c) The extracted text is returned for further processing.
5. ***Boolean Search:***
    <p>a) The boolean_search method performs Boolean searches on the indexed documents.
    <p>b) Tokenize the input query and iterates through its terms.
    <p>c) For each term in the query, it retrieves documents containing that term and performs Boolean operations (AND, OR, NOT) based on the query's structure.

### Program:
```
import numpy as np
import pandas as pd

class BooleanRetrieval:
    def __init__(self):
        self.index = {}
        self.documents_matrix = None
        self.documents = {}

    def index_document(self, doc_id, text):
        self.documents[doc_id] = text
        terms = text.lower().split()
        print("Document -", doc_id, terms)

        for term in terms:
            if term not in self.index:
                self.index[term] = set()
            self.index[term].add(doc_id)

    def create_documents_matrix(self):
        terms = list(self.index.keys())
        num_docs = len(self.documents)
        num_terms = len(terms)

        self.documents_matrix = np.zeros((num_docs, num_terms), dtype=int)

        for i, (doc_id, text) in enumerate(self.documents.items()):
            doc_terms = text.lower().split()
            for term in doc_terms:
                if term in self.index:
                    term_id = terms.index(term)
                    self.documents_matrix[i, term_id] = 1

    def print_documents_matrix_table(self):
        df = pd.DataFrame(self.documents_matrix, columns=self.index.keys())
        print("\nDocument-Term Matrix:\n")
        print(df)

    def print_all_terms(self):
        print("\nAll terms in the documents:")
        print(list(self.index.keys()))

    def boolean_search(self, query):
        query = query.lower().split()
        result = set(self.documents.keys())

        i = 0
        while i < len(query):
            term = query[i]

            if term == "and":
                i += 1
                next_term = query[i]
                result = result.intersection(self.index.get(next_term, set()))

            elif term == "or":
                i += 1
                next_term = query[i]
                result = result.union(self.index.get(next_term, set()))
            elif term == "not":
                i += 1
                next_term = query[i]
                result = result.difference(self.index.get(next_term, set()))
            else:
                result = self.index.get(term, set())
            i += 1
        return result


# Main Program
if __name__ == "__main__":

    indexer = BooleanRetrieval()

    documents = {
        1: "Python is a programming language",
        2: "Information retrieval deals with finding information",
        3: "Boolean models are used in information retrieval"
    }

    # Indexing documents
    for doc_id, text in documents.items():
        indexer.index_document(doc_id, text)

    # Create document-term matrix
    indexer.create_documents_matrix()
    indexer.print_documents_matrix_table()
    indexer.print_all_terms()

    # Boolean Search
    query = input("\nEnter your boolean query: ")
    results = indexer.boolean_search(query)

    if results:
        print(f"\nResults for '{query}': {results}")
    else:
        print("\nNo results found for the query.")
```
### Output:
<img width="1081" height="281" alt="image" src="https://github.com/user-attachments/assets/b06e9a93-c9f7-4b94-b6e7-43ef524a46b6" />

<img width="1068" height="286" alt="image" src="https://github.com/user-attachments/assets/4f678bec-745e-43f3-a2c3-cb487915a3a6" />

<img width="1123" height="276" alt="image" src="https://github.com/user-attachments/assets/93f97bc4-d2c2-44dd-8800-e76418b3880c" />

<img width="1087" height="274" alt="image" src="https://github.com/user-attachments/assets/ff9f4e25-0d9e-49cd-9a07-b7b7615c1414" />

<img width="1144" height="278" alt="image" src="https://github.com/user-attachments/assets/ca1b8f22-b7a8-47d0-b392-2d9114a3c024" />

### Result:
Thus,Information Retrieval Using Boolean Model in Python is successfully verified.
