### iterator패턴
뭔가 많이 모여있는 것들을 순서대로 지정면서 전체를 검색하는 처리를 하기 위한 것

> 반복문을 재사용 하기 위한 패턴

### 클래스 다이어 그램
- Aggregate는 인터페이스로 iteraotr인터페이스를 생성한다.
- iterator인터페이스는 BookShelfIterator를 자식으로 갖는다.
- BookShelfIterator는 BookShelf를 배열의 원소로 갖고 BookShelf는 Book를 배열의 원소로 갖는다.


```
public interface Aggregate {
    public abstract Iterator iterator();
}
```


```
import java.util.Vector;

public class BookShelf implements Aggregate {
    private Vector books;   
    public BookShelf(int initialsize) {         
        this.books = new Vector(initialsize);   
    }
    public Book getBookAt(int index) {
        return (Book)books.get(index);
    }
    public void appendBook(Book book) {
        books.add(book);
    }
    public int getLength() {
        return books.size();                    
    }
    public Iterator iterator() {
        return new BookShelfIterator(this);
    }
}
```


```
public class BookShelfIterator implements Iterator {
    private BookShelf bookShelf;
    private int index;
    public BookShelfIterator(BookShelf bookShelf) {
        this.bookShelf = bookShelf;
        this.index = 0;
    }
    public boolean hasNext() {
        if (index < bookShelf.getLength()) {
            return true;
        } else {
            return false;
        }
    }
    public Object next() {
        Book book = bookShelf.getBookAt(index);
        index++;
        return book;
    }
}
```


```
public interface Iterator {
    public abstract boolean hasNext();
    public abstract Object next();
}
```

#### main
```
public class Main {
    public static void main(String[] args) {
        BookShelf bookShelf = new BookShelf(4);
        bookShelf.appendBook(new Book("Around the World in 80 Days"));
        bookShelf.appendBook(new Book("Bible"));
        bookShelf.appendBook(new Book("Cinderella"));
        bookShelf.appendBook(new Book("Daddy-Long-Legs"));
        bookShelf.appendBook(new Book("East of Eden"));
        bookShelf.appendBook(new Book("Frankenstein"));
        bookShelf.appendBook(new Book("Gulliver's Travels"));
        bookShelf.appendBook(new Book("Hamlet"));
        Iterator it = bookShelf.iterator();
        while (it.hasNext()) {
            Book book = (Book)it.next();
            System.out.println("" + book.getName());
        }
    }
}
```

#### 출력
```
Around the World in 80 Days
Bible
Cinderella
Daddy-Long-Legs
East of Eden
Frankenstein
Gulliver's Travels
Hamlet
```

