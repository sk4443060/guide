✅ Pehle samajhiye: Class vs Object
   📦 Class = Design (blueprint)
      Jaise ek Car ka design.

   🚗 Object = Real item based on that design
      Jaise ek Honda Car, jo us design (class) se bani hai.

✅ :: (Scope Resolution Operator)
  🔧 Use for: Class ke static method ya constant ko call karne ke liye.
  📌 Kya hota hai? Aap direct class se kuch call karte ho, object banaye bina.

  Example

    class MathHelper {
        public static function square($number) {
            return $number * $number;
        }
    }
    
    // Call using ::
    echo MathHelper::square(5);  // Output: 25

  📸 Pictorial View:

    +-----------------+
    |   MathHelper    |  ← Class (Blueprint)
    +-----------------+
    | + square()      |  ← Static method
    +-----------------+
    
    Usage:
    MathHelper::square(5)
             ↑
         Class name

✅ -> (Object Operator)
  🔧 Use for: Object ke method ya property ko call karne ke liye.
  📌 Kya hota hai? Pehle aap object banate ho, phir us se kuch call karte ho.

  Example

    class Car {
        public function drive() {
            return "Car is moving";
        }
    }
    
    $myCar = new Car();        // ← Object bana
    echo $myCar->drive();      // ← Object se method call

  📸 Pictorial View:

    +--------+        new Car()         +--------------------+
    |  Car   |  --------------------→  |   $myCar (object)  |
    +--------+                         +--------------------+
    | drive()|                         |  drive() method    |
    +--------+                         +--------------------+
    
    Usage:
    $myCar->drive()
            ↑
         Object name

  🧠 Ek Simple Trick Yaad Rakhne Ki:

    | Operator | Use When You're Working With | Example                             |
    | -------- | ---------------------------- | ----------------------------------- |
    | `::`     | **Class directly**           | `Route::get()`                      |
    | `->`     | **Object/Instance**          | `$car->drive()` or `->middleware()` |
