## Task 1
Implement User class so the following code outputs “John Doe <john.doe@example.com>“:
```
class User
 {
        // MAKE AN IMPLEMENTATION
}
$user = new User();
$user->setFirstName(‘John’)
   ->setLastName(‘Doe’)
   ->setEmail('john.doe@example.com’)
;
echo $user;
```

## Task 2
There is a code supporting calculation if a car is damaged.
Now it should be extended to support calculating if a painting of car’s exterior is damaged (this means, if a painting of any of car details is not OK - for example a door is scratched).
```
<?php
abstract class CarDetail {
   protected $isBroken;
   public function __construct(bool $isBroken)
   {
       $this->isBroken = $isBroken;
   }
   public function isBroken(): bool
   {
       return $this->isBroken;
   }
}
class Door extends CarDetail
{
}
class Tyre extends CarDetail
{
}
class Car
{
   /**
    * @var CarDetail[]
    */
   private $details;
   /**
    * @param CarDetail[] $details
    */
   public function __construct(array $details)
   {
       $this->details = $details;
   }
   public function isBroken(): bool
   {
       foreach ($this->details as $detail) {
           if ($detail->isBroken()) {
               return true;
           }
       }
       return false;
   }
   public function isPaintingDamaged(): bool
   {
       // MAKE AN IMPLEMENTATION
   }
}
$car = new Car([new Door(true), new Tyre(false), ....]); // we pass a list of all details
```
Expected result: an implemented code.
Note: you are allowed (and encouraged) to change anything in the existing code in order to make an implementation SOLID compliant

## Task 3
Please take a look at the code below. We’ve got a class FightService, which implements a logic of a fight between two heroes. After the fight one of the hero may lose some health points.
Please implement a test for FightService::fight() method.
Feel free to refactor any code if you think it’s needed.
```
<?php
use PHPUnit\Framework\TestCase;
interface HeroInterface
{
   public function getAttack(): int;
   public function getDefence(): int;
   public function getHealthPoints(): int;
   public function setHealthPoints(int $healthPoints);
}
class DamageCalculator
{
   const DAMAGE_RAND_FACTOR = 0.2;
   public static function calculateDamage(HeroInterface $attacker, HeroInterface $defender): int
   {
       $damage = 0;
       if ($attacker->getAttack() > $defender->getDefence()) {
           $baseDamage = $attacker->getAttack() - $defender->getDefence();
           $factor = $baseDamage * self::DAMAGE_RAND_FACTOR;
           $minDamage = $baseDamage - $factor;
           $maxDamage = $baseDamage + $factor;
           $damage = mt_rand($minDamage, $maxDamage);
       }
       return $damage;
   }
}
class FightService
{
   public function fight(HeroInterface $attacker, HeroInterface $defender)
   {
       $damage = DamageCalculator::calculateDamage($attacker, $defender);
       $defender->setHealthPoints($defender->getHealthPoints() - $damage);
   }
}
class FightServiceTest extends TestCase {
   public function testFight()
   {
       // implement the test
   }
}
```
## Task 4
Imagine we design a marketplace solution for selling strawberries.
Over public API any seller should be able to add a lot with strawberries.
Each lot may have different weight, a country of origin, harvesting date and a cultivar.
Task: describe REST API endpoints to implement following scenarios:
1) Seller “Best Phones LTD” (id=899) successfully adds lot of “Red Dream” cultivar strawberries, planted in Ukraine and harvested on July 27, 2018 with total weight of 1500 kg.
2) “Delicious strawberries LTD” adds lot of “Red Dream” cultivar strawberries, planted in Ukraine and harvested on July 27, 2018 with total weight of 500 kg, but minimum weight allowed is 1000 kg.
3) “Delicious strawberries LTD” changes harvesting date of created lot to June 14, 2018.

THIS IS NOT A CODING TASK, JUST DESCRIPTION OF ENDPOINTS IS EXPECTED IN RESULT.
Each endpoint description should contain URL, request/response payload and response status code.
Authentication, authorisation and registration for sellers and buyers are out of the task scope.
