class Book:
    def __init__(self, title, author, isbn, quantity):
        self.title = title
        self.author = author
        self.isbn = isbn
        self.quantity = quantity
    
    def __str__(self):
        return f"Title: {self.title}, Author: {self.author}, ISBN: {self.isbn}, Quantity: {self.quantity}"

class Library:
    def __init__(self):
        self.books = []

    def add_book(self, title, author, isbn, quantity):
        book = Book(title, author, isbn, quantity)
        self.books.append(book)
        print(f"Book '{title}' added successfully!")

    def list_books(self):
        if not self.books:
            print("No books available in the library.")
            return
        for idx, book in enumerate(self.books):
            print(f"{idx+1}. {book}")

    def borrow_book(self, isbn):
        for book in self.books:
            if book.isbn == isbn:
                if book.quantity > 0:
                    book.quantity -= 1
                    print(f"You have borrowed '{book.title}'. Enjoy your reading!")
                    return
                else:
                    print(f"Sorry, '{book.title}' is currently out of stock.")
                    return
        print("Book with that ISBN not found.")

    def return_book(self, isbn):
        for book in self.books:
            if book.isbn == isbn:
                book.quantity += 1
                print(f"Thank you for returning '{book.title}'.")
                return
        print("Book with that ISBN not found.")

    def search_book(self, title=None, author=None, isbn=None):
        found_books = []
        for book in self.books:
            if (title and title.lower() in book.title.lower()) or \
               (author and author.lower() in book.author.lower()) or \
               (isbn and isbn == book.isbn):
                found_books.append(book)

        if found_books:
            for book in found_books:
                print(book)
        else:
            print("No books found matching the search criteria.")

def main():
    library = Library()

    while True:
        print("\nLibrary Management System")
        print("1. Add Book")
        print("2. List Available Books")
        print("3. Borrow Book")
        print("4. Return Book")
        print("5. Search Books")
        print("6. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            title = input("Enter book title: ")
            author = input("Enter author name: ")
            isbn = input("Enter ISBN: ")
            quantity = int(input("Enter quantity: "))
            library.add_book(title, author, isbn, quantity)
        elif choice == "2":
            library.list_books()
        elif choice == "3":
            isbn = input("Enter ISBN of the book to borrow: ")
            library.borrow_book(isbn)
        elif choice == "4":
            isbn = input("Enter ISBN of the book to return: ")
            library.return_book(isbn)
        elif choice == "5":
            search_choice = input("Search by (T)itle, (A)uthor, or (I)SBN: ").lower()
            if search_choice == "t":
                title = input("Enter title to search: ")
                library.search_book(title=title)
            elif search_choice == "a":
                author = input("Enter author to search: ")
                library.search_book(author=author)
            elif search_choice == "i":
                isbn = input("Enter ISBN to search: ")
                library.search_book(isbn=isbn)
            else:
                print("Invalid choice.")
        elif choice == "6":
            print("Exiting the system. Goodbye!")
            break
        else:
            print("Invalid choice! Please try again.")

if __name__ == "__main__":
    main()
