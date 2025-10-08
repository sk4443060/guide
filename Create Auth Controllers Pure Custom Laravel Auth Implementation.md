We’ll create 3 controllers:
RegisterController
LoginController
LogoutController

Run commands:

    php artisan make:controller Auth/RegisterController
    php artisan make:controller Auth/LoginController
    php artisan make:controller Auth/LogoutController

Define Routes
Open:
routes/web.php

    use App\Http\Controllers\Auth\RegisterController;
    use App\Http\Controllers\Auth\LoginController;
    use App\Http\Controllers\Auth\LogoutController;
    use Illuminate\Support\Facades\Route;
    
    Route::get('/', function () {
        return view('welcome');
    });
    
    // Register
    Route::get('/register', [RegisterController::class, 'showRegisterForm'])->name('register.form');
    Route::post('/register', [RegisterController::class, 'register'])->name('register');
    
    // Login
    Route::get('/login', [LoginController::class, 'showLoginForm'])->name('login.form');
    Route::post('/login', [LoginController::class, 'login'])->name('login');
    
    // Logout
    Route::post('/logout', [LogoutController::class, 'logout'])->name('logout');
    
    // Dashboard (protected route)
    Route::get('/dashboard', function () {
        return view('dashboard');
    })->middleware('auth')->name('dashboard');

Register Controller
file: app/Http/Controllers/Auth/RegisterController.php

    namespace App\Http\Controllers\Auth;

    use App\Http\Controllers\Controller;
    use Illuminate\Http\Request;
    use App\Models\User;
    use Illuminate\Support\Facades\Hash;
    use Illuminate\Support\Facades\Auth;
    
    class RegisterController extends Controller
    {
        public function showRegisterForm()
        {
            return view('auth.register');
        }
    
        public function register(Request $request)
        {
            $request->validate([
                'name' => 'required|min:3',
                'email' => 'required|email|unique:users',
                'password' => 'required|min:6|confirmed'
            ]);
    
            $user = User::create([
                'name' => $request->name,
                'email' => $request->email,
                'password' => Hash::make($request->password),
            ]);
    
            Auth::login($user);
    
            return redirect()->route('dashboard');
        }
    }

Login Controller
File: app/Http/Controllers/Auth/LoginController.php

    namespace App\Http\Controllers\Auth;

    use App\Http\Controllers\Controller;
    use Illuminate\Http\Request;
    use Illuminate\Support\Facades\Auth;
    
    class LoginController extends Controller
    {
        public function showLoginForm()
        {
            return view('auth.login');
        }
    
        public function login(Request $request)
        {
            $credentials = $request->validate([
                'email' => 'required|email',
                'password' => 'required'
            ]);
    
            if (Auth::attempt($credentials)) {
                $request->session()->regenerate();
                return redirect()->intended('dashboard');
            }
    
            return back()->withErrors([
                'email' => 'Invalid credentials.',
            ]);
        }
    }

Logout Controller
File: app/Http/Controllers/Auth/LogoutController.php

    namespace App\Http\Controllers\Auth;

    use App\Http\Controllers\Controller;
    use Illuminate\Http\Request;
    use Illuminate\Support\Facades\Auth;
    
    class LogoutController extends Controller
    {
        public function logout(Request $request)
        {
            Auth::logout();
            $request->session()->invalidate();
            $request->session()->regenerateToken();
            return redirect('/');
        }
    }

Blade Files
Create folder:
resources/views/auth/
  register.blade.php
  
      <!DOCTYPE html>
      <html>
        <head>
            <title>Register</title>
        </head>
        <body>
          <h2>Register</h2>
          <form method="POST" action="{{ route('register') }}">
              @csrf
              <input type="text" name="name" placeholder="Name" required><br><br>
              <input type="email" name="email" placeholder="Email" required><br><br>
              <input type="password" name="password" placeholder="Password" required><br><br>
              <input type="password" name="password_confirmation" placeholder="Confirm Password" required><br><br>
              <button type="submit">Register</button>
          </form>
          <a href="{{ route('login.form') }}">Already have an account? Login</a>
        </body>
      </html>

  login.blade.php

      <!DOCTYPE html>
      <html>
        <head>
            <title>Login</title>
        </head>
        <body>
          <h2>Login</h2>
          <form method="POST" action="{{ route('login') }}">
              @csrf
              <input type="email" name="email" placeholder="Email" required><br><br>
              <input type="password" name="password" placeholder="Password" required><br><br>
              <button type="submit">Login</button>
          </form>
          <a href="{{ route('register.form') }}">Don't have an account? Register</a>
        </body>
      </html>

dashboard.blade.php

    <!DOCTYPE html>
    <html>
      <head>
          <title>Dashboard</title>
      </head>
      <body>
        <h2>Welcome, {{ Auth::user()->name }}</h2>
        
        <form method="POST" action="{{ route('logout') }}">
            @csrf
            <button type="submit">Logout</button>
        </form>
      </body>
    </html>

Middleware Check

Laravel already has auth middleware.
Check file: app/Http/Middleware/Authenticate.php
It redirects unauthorized users to /login.

🧭 FLOW DIAGRAM

    User → Register Form → RegisterController → DB → Login (Auto) → Dashboard
    User → Login Form → LoginController → Auth::attempt() → Dashboard
    User → Logout → Session Destroy → Redirect to Home

    +------------+     +------------------+     +-------------+
    |  Register  | --> |  Validate Input  | --> |  Create User|
    +------------+     +------------------+     +-------------+
                                                   |
                                                   v
                                             +------------+
                                             |  Login User|
                                             +------------+
                                                   |
                                                   v
                                             +-------------+
                                             |  Dashboard  |
                                             +-------------+

⚙️ BONUS: Forgot Password (Optional Extension)

If you want to add forgot/reset manually, you can later integrate Laravel’s built-in Password::sendResetLink() methods or mailables.

✅ FINAL OUTPUT:

/register → User registration
/login → User login
/dashboard → Protected page (only for logged-in users)
/logout → Ends session
