<h2> Intro: </h2>
To build off of my SRP blog post, I would like to take the opportunity to explore the Open/Closed Principle of the SOLID Principles of Object Oriented Design. I'm going to refer back to the Art Gallery example that I used in my SRP blog post and build off that example to explore the Open/Closed Principle. The Open/Closed principle states that software should be open for extension and closed for modification. The basic idea is that we shouldn't want to change code that is tested and works, but instead we want to extend its functionality by building off of it. Lets explore our previous example and see how this applies.

<h2> Open/Closed Principle Example </h2>
Lets return to the art gallery as our curators would like to add some additional functionality to the software we built for them. This is what we have so far:

    class Artwork

      def get_title title
        title
      end

      def get_artist artist
        artist
      end

      def get_description description
        description
      end

    end

    class Printer

      def print information_to_print
        puts information_to_print
      end

    end

    class Location

      def get_location location
        location
      end

    end

Now, last time we made a few changes to adhere to SRP. We don't want to change this code in any way that would jeopardize its functionality as we know it works.

Lets say the curators want to be able to organize the artwork into groups, such as sculptures and paintings and they need similar attributes from artwork such as the title, artist, and description. Well, we can do that using inheritance! We can make additional classes that extend our artwork class and utilize its methods. So here we are extending the functionality (Open) and not disrupting the current functionality (Closed).

    class Artwork

      def get_title title
        title
      end

      def get_artist artist
        artist
      end

      def get_description description
        description
      end

    end

    class Sculpture < Artwork

    end

    class Painting < Artwork

    end

    class Printer

      def print information_to_print
        puts information_to_print
      end

    end

    class Location

      def get_location location
        location
      end

    end

We can now utilize the methods from artwork into our Sculpture and Painting classes as they will inherit them. We have extended our software's functionality. Our new classes can also use the Printer and Location classes since we pulled them from the Artwork class in the SRP blog post. 

<h2> Conclusion </h2>
We have now extended the functionality of our software, but we did not modify our older code. We have followed the Open/Closed principle and now our code is much cleaner for it. If things change in the future, as they tend to do, we can continue to extend the functionality of our code. The Open/Closed Principle is definitely an important piece to clean OO code.