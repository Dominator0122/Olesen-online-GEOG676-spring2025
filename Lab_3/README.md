# Olesen-online-GEOG676-spring2025
Dom Olesen GEOG676

# Create classes
class Shape:
    def __init__(self):
        pass

class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def getArea(self):
        return self.length * self.width

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def getArea(self):
        return 3.14 * self.radius * self.radius

class Triangle(Shape):
    def __init__(self, base, height):
        self.base = base
        self.height = height

    def getArea(self):
        return 0.5 * self.base * self.height


# Read text file
file_path = r'C:\Users\dom.olesen\OneDrive - Texas A&M AgriLife\Desktop\Spring_2025\Geog_676\Lab3\shape.txt'
with open(file_path, 'r') as file:
    lines = file.readlines()

for line in lines:
    components = line.strip().split(',')  
    shape = components[0]

    if shape == 'Rectangle':
        rect = Rectangle(int(components[1]), int(components[2]))  
        print('Area of Rectangle is:', rect.getArea())
    elif shape == 'Circle':
        cirl = Circle(int(components[1]))  
        print('Area of Circle is:', cirl.getArea())
    elif shape == 'Triangle':
        tri = Triangle(int(components[1]), int(components[2]))  
        print('Area of Triangle is:', tri.getArea())
    else:
        pass

