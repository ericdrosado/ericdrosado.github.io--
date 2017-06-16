<h2> Intro: </h2>
In continuing our journey through the SOLID Principles of OOD, I'd like to address the Liskov Substitution Principle. This principle is very straightforward and it allows me an oportunity to build off my Open/Closed Principle post. The Liskov Substitution Principle states that subclasses should have the ability to substitute for their parent classes in a class heirarchy. Let's look at the Open/Closed example and build off that.

<h2> Liskov Substitution Principle Example </h2>
Last time in the Open/Closed Principle blog post we introduced some new classes and we now have the following:
    
    Class Artwork

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

    Class Sculpture < Artwork

    end

    Class Painting < Artwork

    end

        Class Printer

          def print information_to_print
            puts information_to_print
          end

        end

        Class Location

          def get_location location
            location
          end

        end

Let's not worry about the Printer and Location classes and remove them for now and lets focus on the class hierarchy:

    Class Artwork

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

    Class Sculpture < Artwork

    end

    Class Painting < Artwork

    end

Here we have classes that inherit directly from Artwork, but they do not have methods of their own. Let's say that in the sculpting word there are no such things as titles, but instead they like to call them names instead of titles. This example is a bit of a stretch, but we don't have a name method in artwork in order for a sculpture to inherit. Perhaps we should motify get_title in sculpture and override it, but that would defeat the purpose of the inheritance.

Ultimately we have the wrong abstration here, meaning perhaps we need to extend our Artwork class to have artwork with names and another with titles so that sculpture might work. We cannot substitute sculpture into Artwork because of this difference.

So, that example might be a little hard to swallow. Lets look at another example that is commonly used:

    Class Rectangle

      def get_width
      end

      def get_height
      end

    end

    Class Square < Rectangle

    end

This might not look like a problem, but does it make sense that the Square class should inherit the two methods in Rectangle? No! With a square you don't need to get a width and height, but just need the length of just one side. Once again, we need another level of abstraction here that can account for Rectangles and one for Squares. Squares cannot substitute in for Rectangles because rectangles have different dimensions. Thus, this breaks Liskov's Substitution Principle.

<h2> Conclusion </h2>
Liskov's Substitution Principle can really help with making sense of your class heirarchies. You can make the appropriate abstractions and allow yourself to have clean OO code.
