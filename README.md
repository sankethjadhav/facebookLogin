# facebookLogin

import UIKit
//1import FacebookLogin
import FBSDKCoreKit
import FBSDKLoginKit
class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        
        
        // Do any additional setup after loading the view, typically from a nib.
    }

    @IBAction func facebookSignIn(_ sender: Any) {
        let manager = FBSDKLoginManager()
        manager.logOut()
        let fbLoginManager : FBSDKLoginManager = FBSDKLoginManager()
        fbLoginManager.logIn(withReadPermissions: ["email"], from: self) { (result, error) -> Void in
            if (error == nil){
                let fbloginresult : FBSDKLoginManagerLoginResult = result!
                // if user cancel the login
                if (result?.isCancelled)!{
                    return
                }
                if(fbloginresult.grantedPermissions.contains("email"))
                {
                    self.getFBUserData()
                }
            }
        }
        
        
        
    }
    func getFBUserData(){
        if((FBSDKAccessToken.current()) != nil){
            FBSDKGraphRequest(graphPath: "me", parameters: ["fields": "id, name, first_name, last_name, picture.type(large), email"]).start(completionHandler: { (connection, result, error) -> Void in
                if (error == nil){
                    //everything works print the user data
                    
                    let userDetails = result as! NSDictionary
                    
                    
                    
                    
//                    UserDefaults.standard.set(userDetails.value(forKey: "name") as! String, forKey: "name")
//
//                    UserDefaults.standard.set(userDetails.value(forKey: "last_name"), forKey: "familyName")
//
//                    UserDefaults.standard.set(userDetails.value(forKey: "email"), forKey: "email")
//
//                    UserDefaults.standard.set(userDetails.value(forKey: "id") as! String, forKey: "user_id")
//                    UserDefaults.standard.set(((userDetails.value(forKey: "picture")as! NSDictionary).value(forKey: "data") as! NSDictionary).value(forKey: "url")as! String, forKey: "profileImage")
//
//
//                    UserDefaults.standard.synchronize()
                    
                    
                    print(result)
                }
            })
        }
    }
}

podfile


target 'facebookLogin' do
  # Comment the next line if you're not using Swift and don't want to use dynamic frameworks
  use_frameworks!
pod 'FacebookCore'
pod 'FacebookLogin'
pod 'FacebookShare'

  # Pods for facebookLogin

end
