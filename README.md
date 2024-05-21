import sympy as sp

def newton_raphson(fx, dfx, x0, tol=1e-7, max_iter=100):
    """
    Menggunakan metode Newton-Raphson untuk menemukan akar dari fungsi.
    
    :param fx: Fungsi yang ingin dicari akarnya.
    :param dfx: Turunan dari fungsi fx.
    :param x0: Nilai awal tebakan akar.
    :param tol: Toleransi error untuk konvergensi.
    :param max_iter: Maksimum iterasi yang diizinkan.
    :return: Perkiraan akar dan jumlah iterasi yang diperlukan.
    """
    xn = x0
    for n in range(max_iter):
        fxn = fx(xn)
        dfxn = dfx(xn)
        
        if dfxn == 0:
            raise ValueError("Turunan f'(x) bernilai nol, metode gagal.")
        
        xn_next = xn - fxn / dfxn
        
        if abs(xn_next - xn) < tol:
            return xn_next, n + 1
        
        xn = xn_next
    
    raise ValueError("Metode gagal konvergen dalam iterasi maksimum yang diberikan.")

# Contoh penggunaan
if __name__ == "__main__":
    # Definisikan fungsi dan turunannya
    x = sp.symbols('x')
    f = x**2 - 2  # Misalnya, kita ingin mencari akar dari x^2 - 2 = 0
    df = sp.diff(f, x)
    
    # Konversi fungsi simbolik ke fungsi numerik
    f_num = sp.lambdify(x, f)
    df_num = sp.lambdify(x, df)
    
    # Tentukan tebakan awal
    x0 = 1.0
    
    # Panggil metode Newton-Raphson
    akar, iterasi = newton_raphson(f_num, df_num, x0)
    
    print(f"Akar yang ditemukan: {akar}")
    print(f"Jumlah iterasi: {iterasi}")
