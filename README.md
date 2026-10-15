# CMPUT 301: Lab 6 Participation Exercise

## Student Details
- **Full Name:** `Esther Sim`
- **CCID:** `esim1`

## References and Resources
List any resources used here, or simply put `N/A` if not applicable.

## Verbal Collaboration
List students' names and CCIDs here, or simply put `N/A` if not applicable. 


//////////////////////////////////////////////////////////////////////////////////////////
package com.example.lab_6

/**
 * Represents a wizard character that can cast spells using mana.
 *
 * A wizard has a name, current mana, and spell power stat. The
 * wizard needs sufficient mana to cast spells, and spell power
 * is used to calculate how much damage is dealt when a valid
 * spell is cast.
 *
 * @property name the name of the wizard
 * @property mana the current mana available for casting spells
 * @property spellPower the base power used for spell damage calculation
 */
class Wizard(val name: String, var mana: Int, var spellPower: Int) {
    /**
     * Casts a spell and returns the damage dealt
     *
     * Supported spells:
     * - "Explosion": costs 10 mana, deals 3 × spellPower damage
     * - "Frostbite": costs 5 mana, deals 2 × spellPower damage
     *
     * If the wizard does not have enough mana or the spell name is invalid,
     * the spell fails and returns 0.
     *
     * @param spell the name of the spell to cast
     * @return the integer amount of damage dealt, or 0 if the spell fails
     */
    fun castSpell(spell: String): Int {
        when (spell) {
            "Explosion" -> {
                if (mana >= 10) {
                    mana -= 10
                    return spellPower * 3
                } else return 0 // not enough mana
            }
            "Frostbite" -> {
                if (mana >= 5) {
                    mana -= 5
                    return spellPower * 2
                } else return 0 // not enough mana
            }
            else -> {
                return 0 // invalid spell
            }
        }
    }
}

//////////////////////////////////////////////////////////////////////////////////////
package com.example.lab_6

import junit.framework.TestCase.assertEquals
import org.junit.Before
import org.junit.Test

private lateinit var evilWizard: Wizard

// Set up a new wizard before every single test
@Before
fun setUp() {
    evilWizard = Wizard("Evil Wizard", 30, 10)
}

@Test
fun castSpell_explosion_successful() {
    val damageDealt = evilWizard.castSpell("Explosion")

    assertEquals(30, damageDealt) // spellPower of 10 * 3 = 30

    assertEquals(20, evilWizard.mana) // mana of 30 - 10 = 20
}

@Test
fun castSpell_explosion_unsuccessful() {
    evilWizard.mana = 5 // Evil Wizard does not have enough mana to cast "Explosion"
    val damageDealt = evilWizard.castSpell("Explosion")

    assertEquals(0, damageDealt)

    assertEquals(5, evilWizard.mana) // mana still is 5
}

