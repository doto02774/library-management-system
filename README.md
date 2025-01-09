class Book:
    def __init__(self, title, author, book_id):
        self.title = title
        self.author = author
        self.book_id = book_id
        self.is_issued = False

    def issue_book(self):
        if not self.is_issued:
            self.is_issued = True
            print(f'Book "{self.title}" has been issued successfully.')
        else:
            print(f'Sorry, the book "{self.title}" is already issued.')

    def return_book(self):
        if self.is_issued:
            self.is_issued = False
            print(f'Book "{self.title}" has been returned successfully.')
        else:
            print(f'This book "{self.title}" was not issued.')

class Library:
    def __init__(self):
        self.books = []
    
    def add_book(self, title, author):
        book_id = len(self.books) + 1  # Auto-incrementing book ID
        new_book = Book(title, author, book_id)
        self.books.append(new_book)
        print(f'Book "{title}" added to the library with ID: {book_id}')

    def display_books(self):
        if not self.books:
            print("No books available in the library.")
            return
        print("List of Books in the Library:")
        for book in self.books:
            status = "Issued" if book.is_issued else "Available"
            print(f'ID: {book.book_id}, Title: "{book.title}", Author: {book.author}, Status: {status}')
    
    def issue_book(self, book_id):
        for book in self.books:
            if book.book_id == book_id:
                book.issue_book()
                return
        print(f'No book found with ID: {book_id}')
    
    def return_book(self, book_id):
        for book in self.books:
            if book.book_id == book_id:
                book.return_book()
                return
        print(f'No book found with ID: {book_id}')

def menu():
    print("\n--- Library Management System ---")
    print("1. Add Book")
    print("2. Display Books")
    print("3. Issue Book")
    print("4. Return Book")
    print("5. Exit")

def main():
    library = Library()
    
    while True:
        menu()
        choice = input("Enter your choice: ")

        if choice == '1':
            title = input("Enter book title: ")
            author = input("Enter book author: ")
            library.add_book(title, author)
        
        elif choice == '2':
            library.display_books()
        
        elif choice == '3':
            book_id = int(input("Enter book ID to issue: "))
            library.issue_book(book_id)
        
        elif choice == '4':
            book_id = int(input("Enter book ID to return: "))
            library.return_book(book_id)
        
        elif choice == '5':
            print("Exiting the system.")
            break
        
        else:
            print("Invalid choice, please try again.")

if __name__ == "__main__":
    main()
