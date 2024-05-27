
# Library Management System in SQL

## Overview
This project is a Library Management System implemented using SQL. It includes tables for managing books, authors, library branches, borrowers, and book loans, along with stored procedures for common operations.

## Features
- Book Management
- Author Management
- Library Branch Management
- Borrower Management
- Book Loan Management
- Stored Procedures for Common Operations

## Database Schema
The database includes the following tables:
1. `tbl_publisher`
2. `tbl_book`
3. `tbl_library_branch`
4. `tbl_borrower`
5. `tbl_book_loans`
6. `tbl_book_copies`
7. `tbl_book_authors`

## Stored Procedures
### Example: Total Loans Per Branch
Retrieves the branch name and total number of books loaned out from each branch.
#### QUERY:
CREATE PROCEDURE db_LibraryManagement.TotalLoansPerBranch()
BEGIN
    SELECT Branch.library_branch_BranchName AS 'Branch Name', 
           COUNT(Loans.book_loans_BranchID) AS 'Total Loans'
    FROM tbl_book_loans AS Loans
    INNER JOIN tbl_library_branch AS Branch 
        ON Loans.book_loans_BranchID = Branch.library_branch_BranchID
    GROUP BY Branch.library_branch_BranchName;
END;

### Example: Book by Author and Branch
Retrieves the title and number of copies of books by a specific author in a specific branch.
#### QUERY:
CREATE PROCEDURE db_librarymanagement.BookbyAuthorandBranch
    (IN BranchName VARCHAR(50), IN AuthorName VARCHAR(50))
BEGIN
    SELECT Branch.library_branch_BranchName AS 'Branch Name', 
           Book.book_Title AS 'Title', 
           Copies.book_copies_No_Of_Copies AS 'Number of Copies'
    FROM tbl_book_authors AS Authors
    INNER JOIN tbl_book AS Book 
        ON Authors.book_authors_BookID = Book.book_BookID
    INNER JOIN tbl_book_copies AS Copies 
        ON Authors.book_authors_BookID = Copies.book_copies_BookID
    INNER JOIN tbl_library_branch AS Branch 
        ON Copies.book_copies_BranchID = Branch.library_branch_BranchID
    WHERE Branch.library_branch_BranchName = BranchName 
        AND Authors.book_authors_AuthorName = AuthorName;
END;

### Usage:
1. Create the database and tables.
2. Insert initial data.
3. Create the stored procedures.
4. Execute the procedures to retrieve and manipulate data.


