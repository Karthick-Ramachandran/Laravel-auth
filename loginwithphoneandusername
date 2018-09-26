<!---
public function login(Request $request){ 


        $validator = Validator::make($request->all(), [
            'login' => 'required',
            'password' => 'required'
        ]);
 
        if ($validator->fails()) {
            return response()->json(['status' => 'Failed',
            'error'=>$validator->errors()], 200);            
        }
        $field = filter_var($request->input('login'), FILTER_VALIDATE_EMAIL) ? 'email' : 'phone';
        $request->merge([$field => $request->input('login')]);
 
        if(Auth::attempt($request->only($field, 'password'))){
            $user = Auth::user();

            $success['Firstname'] =  $user->fname;
            $success['Lastname'] =  $user->lname;
            $success['Mobile'] =  $user->phone;
            $success['Email'] =  $user->email;
            $success['id'] =  $user->id;
            $success['token'] =  $user->createToken('MyApp')->accessToken;
            $success['image'] = "";

            return response()->json([ 'status' => 'Success' ,'success' => $success], 200);
        }
        else{
            return response()->json(['status' => 'failed',
            'error'=>'Email or Password is Incorrect, Unauthorized'], 200);
        }
    }
    
    -->
