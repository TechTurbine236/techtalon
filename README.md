# techtalon
talon
import json
import os

class Book:
    def __init__(self, title, author, year):
        self.title = title
        self.author = author
        self.year = year

    def __str__(self):
        return f"'{self.title}' by {self.author} ({self.year})"

class Library:
    def __init__(self, filename="library.json"):
        self.filename = filename
        self.books = []
        self.load_books()

    def load_books(self):
        if os.path.exists(self.filename):
            with open(self.filename, "r") as file:
                books_data = json.load(file)
                self.books = [Book(**data) for data in books_data]
        else:
            self.books = []

    def save_books(self):
        with open(self.filename, "w") as file:
            json.dump([book.__dict__ for book in self.books], file, indent=4)

    def add_book(self, title, author, year):
        new_book = Book(title, author, year)
        self.books.append(new_book)
        self.save_books()

    def remove_book(self, title):
        self.books = [book for
