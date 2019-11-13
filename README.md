# Lab_8_BookCase

CIS 3515 Assignment Worksheet 8
Instructions: Create a new GitHub Branch and update your BookCase app with new features.
You application will use a Web Service API (See Appendix below) to fetch book information, and display that information in its various modes. You application will allow a user to retrieve all available book titles available via the API, as well as allow a user to search for a subset of titles that match a user-proved search string.
1. Create a Book class in your application that contains the following fields for a book:
1. id: int – A system provided ID for the book
2. title: String – The title of the book
3. author: String – The author of the book
4. published: int – The year the book was published
5. coverURL: String – A URL to the image representing the book cover
2. Use either an ArrayList (ArrayList<Book>) or your own collection class to keep a collection of book objects.
3. Modify BookDetailsFragment to accept a Book object instead of just a String title, and have it display the book cover image, the book title, the author and the year published.
4. Modify your main activity to query the provided book search API when your activity loads. When queried, the API will return all available books. The returned titles should be used to populate the collection of books (requirement 2), and allow the user to browse
1. This start-up query should only be performed the first time the activity loads – If the activity is reloaded (because of a configuration change, such as rotating the device), then the activity should not reload the data, but should instead fetch the list of books from the last fragment that contained it. More information is provided in the next item.
5. Modify your BookListFragment and your ViewPagerFragment to have a public method that returns the list of books that it is currently displaying. From time to time the activity may fetch the set of books from one fragment and pass it to another. We are relying on the fact that fragments are retained during activity restarts.
6. In your activity, add a search function (An EditText to allow the user to enter a search term, and a button to begin the search).
1. When a user performs a search, they will receive a subset of books which may include zero, some, or all available books.

2. A user can search for books based on title, author, or published year
3. When a search result is returned, the collection of books being displayed to the user should be updated to only show the books returned
4. Once the list of books have been searched for and the display updated (whether being displayed in a ListView or a ViewPager), that subset of books must always be displayed until the user performs a new search, even if the activity is restarted. Utilize the public method mentioned in Item 5 to fetch the books from a fragment A, when that fragment is about to be replaced with a fragment B.
7. Push your project to GitHub and upload the link to the new repository branch to Canvas.

CONSIDERATIONS
1) When updating a FragmentStatePagerAdapter with new data, a “bug” in the Android framework fails to refresh the displayed data when notifyDataSetChanged() in called. A known workaround is to override the adapter’s getItemPosition() method as follows:
@Override
public int getItemPosition(@NonNull Object object) { return PagerAdapter.POSITION_NONE;
}
2) When placing data inside bundles to use as arguments for fragments, you might notice that most of the setter methods are for primitive data types. When you need to pass non-primitive data types (which may be the case in this app since you might end up passing around Book objects and collections), you need to ensure that the class whose objects you intend to pass implements one of the compatible interfaces, such as Parcelable (https://developer.android.com/reference/android/os/Parcelable), or Serializable (https://developer.android.com/reference/java/io/Serializable). When you implement one of these interfaces, you can use bundle setter methods to place objects of those class types inside a bundle object. Eg:
Bundle bundle = new Bundle(); bundle.putParcelable("myBook", book);
or
Bundle bundle = new Bundle();
ArrayList<Book> books = getBooks(); bundle.putParcelableArrayList("myBooks", books);
  
Appendix
BookCase API
Get full list of books in JSON format: https://kamorris.com/lab/audlib/booksearch.php
Get subset of books based on search string in JSON format: https://kamorris.com/lab/audlib/booksearch.php?search=<search_string>

