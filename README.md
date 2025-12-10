"""
Package Sorter for Thoughtful's Robotic Automation Factory
Author: Ahmed
Date: 2025-12-10
"""

def sort(width: float, height: float, length: float, mass: float) -> str:
    """
    Determines the stack for a package based on its dimensions and mass.

    Parameters:
    width (cm), height (cm), length (cm) : float - package dimensions
    mass (kg) : float - package weight

    Returns:
    str: "STANDARD", "SPECIAL", or "REJECTED"
    """
    volume = width * height * length
    is_bulky = volume >= 1_000_000 or max(width, height, length) >= 150
    is_heavy = mass >= 20

    if is_bulky and is_heavy:
        return "REJECTED"
    elif is_bulky or is_heavy:
        return "SPECIAL"
    else:
        return "STANDARD"


# Simple test cases
if __name__ == "__main__":
    test_cases = [
        (50, 50, 50, 10, "STANDARD"),  # normal
        (200, 50, 50, 10, "SPECIAL"),  # bulky
        (50, 50, 50, 25, "SPECIAL"),   # heavy
        (200, 200, 50, 25, "REJECTED"),# bulky + heavy
        (100, 100, 100, 19, "SPECIAL"),# bulky by volume only
    ]

    for w, h, l, m, expected in test_cases:
        result = sort(w, h, l, m)
        print(f"sort({w},{h},{l},{m}) = {result} | Expected: {expected} | {'PASS' if result == expected else 'FAIL'}")
