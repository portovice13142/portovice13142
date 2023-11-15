def C3_representation(n, is_prime=False, starting_prime=2):
    if n < 0:
        n *= -1
    if n == 3:
        return "1^2 + (1 * 1) + 1^2 = 3"
    if (n % 6 == 1) and (is_prime or sympy.isprime(n)):
        # Find the first non-cubic residue mod n
        divisible3 = 0
        m = n + (-1)
        while (m) % 3 == 0:
            m //= 3
            divisible3 += 1
        m = n + (-1)
        g = starting_prime
        while True:
            z = (pow(g, (m) // 3**divisible3, n))
            if 3 * g > n:
                return "The value is not a prime, so probably there is no C3 representation for the value"
            if z == 1:
                #print(f"\033[33m{(g)}\033[0m")
                g = sympy.nextprime(g)
                continue
            count = 0
            while True:
                if count > divisible3:
                    return "The value is not a prime, so probably there is no C3 representation for the value"
                if pow(z, 2, n) == n + ((-1) * (z + 1)):
                    #print(f"\033[94m{(g)}\033[0m")
                    break
                else:
                    z = pow(z, 3, n)
                    count += 1
            break
        a0 = z
        a1 = n + (-a0)
        a0, a1 = max(a0, a1), min(a0, a1)
        # Initialize variables
        a_i_minus_1 = a0
        a_i = a1
        # Iterate until reaching a value lower than the square root of n
        while a_i * a_i + a_i >= n:
            #print(f"\033[33m{(a_i)}\033[0m")
            a_i_minus_1, a_i = a_i, a_i_minus_1 % a_i
        #print(f"\033[94m{(a_i)}\033[0m")
        # Return the C3 representation
        x = a_i
        y = (x * z) % n
        if 2 * y > n:
            y = n + ((-1) * (x + y))
        x, y = max(x, y), min(x, y)
        if x**2 + (x * y) + y**2 == n:
            return f"{(x)}^2 + ({(x)} * {(y)}) + {(y)}^2 = {(n)}"
        else:
            return "The value is not a prime, so probably there is no C3 representation for the value"
    else:
        return "The value is not a prime, or it is 2 mod 3, so no C3 representation exists"
    
def C4_representation(n, is_prime=False, starting_prime=2):
    if n < 0:
        n *= -1
    if n == 2:
        return "1^2 + 1^2 = 2"
    if (n % 4 == 1) and (is_prime or sympy.isprime(n)):
        # Find the first non-quadratic residue mod n
        divisible2 = 0
        m = n + (-1)
        while (m) % 2 == 0:
            m //= 2
            divisible2 += 1
        m = n + (-1)
        g = starting_prime
        while True:
            z = (pow(g, (m) // 2**divisible2, n))
            if 2 * g > n:
                return "The value is not a prime, so probably there is no C4 representation for the value"
            if z == 1 or z == n + (-1):
                #print(f"\033[33m{(g)}\033[0m")
                g = sympy.nextprime(g)
                continue
            count = 0
            while True:
                if count > divisible2:
                    return "The value is not a prime, so probably there is no C4 representation for the value"
                if pow(z, 2, n) == n + (-1):
                    #print(f"\033[94m{(g)}\033[0m")
                    break
                else:
                    z = pow(z, 2, n)
                    count += 1
            break
        a0 = z
        a1 = n + (-a0)
        a0, a1 = max(a0, a1), min(a0, a1)
        # Initialize variables
        a_i_minus_1 = a0
        a_i = a1
        # Iterate until reaching a value lower than the square root of n
        while a_i * a_i >= n:
            #print(f"\033[33m{(a_i)}\033[0m")
            a_i_minus_1, a_i = a_i, a_i_minus_1 % a_i
        #print(f"\033[94m{(a_i)}\033[0m")
        # Return the C4 representation
        x = a_i
        y = (a_i * a1) % n
        if 2 * y > n:
            y = n + (-y)
        x, y = max(x, y), min(x, y)
        if x**2 + y**2 == n:
            return f"{(x)}^2 + {(y)}^2 = {(n)}"
        else:
            return "The value is not a prime, so probably there is no C4 representation for the value"
    else:
        return "The value is not a prime, or it is 3 mod 4, so no C4 representation exists"
