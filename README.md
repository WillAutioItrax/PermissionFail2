# PermissionFail2
XF sample of how Permissions.CheckStatusAsync fails in UWP

This is a simple repo of what I am getting in my app. 
I started with a Visual Studio Xamarin Forms master-detail template app out of the box. In the AboutPage.xaml I added a Label and in AboutPage.xaml.cs I added an onAppearing() like this:

        protected override async void OnAppearing()
        {
            base.OnAppearing();
            PermissionStatus status5 = await Permissions.CheckStatusAsync
                <Permissions.LocationWhenInUse>().ConfigureAwait(false);

            TestLabel.Text = "Something";
        }

This code results in an exception:
'The application called an interface that was marshalled for a different thread. (Exception from HRESULT: 0x8001010E (RPC_E_WRONG_THREAD))'
at
TestLabel.Text = "Something";

If I remove the .ConfigureAwait(false) then it works fine. 
The reason that I have the ConfigureAwait is because in my app, I get intellisense telling me to add ConfigureAwait. So I did. And I got the crashing.
