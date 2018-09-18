# Laravel-auth
Laravel Auth API



<?php

namespace App\Http\Controllers;
use Auth;

use App\User;
use Illuminate\Http\Request;

use Validator;

use GuzzleHttp\Psr7\Response;

class ApiRegisterController extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index(Request $request)
    {
        $this->validate($request,
        [
            'fname' => 'required|string|max:255',
            'lname' => 'required|string|max:255',
             'password' => 'required|string|min:6|confirmed',
             'email' => 'required|string|email|max:255|unique:users',
             'phone' => 'required|numeric|unique:users',
             'lname' => 'required|string|max:255',
             'address' => 'required',
             'district' => 'required',
             'city' => 'required',
             'taluk' => 'required',
             'pincode' => 'required',
 
        ],
        
        [
            'fname.required'=>"Enter your Name",
            'lname.required'=>"Enter your Name",
            'address.required'=>"Enter your address",
            'district.required'=>"Enter your district",
            'city.required'=>"Enter your city",
            'taluk.required'=>"Enter your taluk",
            'pincode.required'=>'Enter  one Pincode',
            'description.required'=>'chosse  one admin',
            ]); //
             $admin = new User;
            $admin->fname=$request->input('fname');
            $admin->lname=$request->input('lname');
            $admin->email=$request->input('email');
            $admin->password=bcrypt($request->input('password'));
            $admin->phone=$request->input('phone');
            $admin->address=$request->input('address');
            $admin->district=$request->input('district');
            $admin->city=$request->input('city');
            $admin->taluk=$request->input('taluk');
            $admin->pincode=$request->input('pincode');
            $admin->status=1;
            $admin->deleted_on_off=1;
            $admin->role_id=2;
            $admin->admin=0;
            $admin->created_at= new \DateTime();
            $admin->save();
            $success['token'] = $admin->createToken('MyApp')->accessToken;
            $success['name'] = $admin->fname;
       return response()->json(['success'=>$success], 200);
    }

    /**
     * Show the form for creating a new resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function login(Request $request){ 


        $validator = Validator::make($request->all(), [
            'email' => 'required|email',
            'password' => 'required'
        ]);
 
        if ($validator->fails()) {
            return response()->json(['error'=>$validator->errors()], 401);            
        }
 
        if(Auth::attempt(['email' => request('email'), 'password' => request('password')])){
            $user = Auth::user();
            $success['token'] =  $user->createToken('MyApp')->accessToken;
            return response()->json(['success' => $success], 200);
        }
        else{
            return response()->json(['error'=>'Unauthorised'], 401);
        }
    }

    /**
     * Store a newly created resource in storage.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return \Illuminate\Http\Response
     */
    public function store(Request $request)
    {
        //
    }

    /**
     * Display the specified resource.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function show($id)
    {
        
        
    $complaint = Complaint::FindorFail($id);


        


    }

    /**
     * Show the form for editing the specified resource.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function edit($id)
    {
        //
    }

    /**
     * Update the specified resource in storage.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function update(Request $request, $id)
    {
        // 
        // JS Laravel 

    }

    /**
     * Remove the specified resource from storage.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function destroy($id)
    {
        //  API. Resources

    }
}

