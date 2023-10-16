# windows-hive-parser-lib

Example Usage:
```c
int main( ) {
	const auto parser = hive_parser( R"(C:\regdump\SYSTEM)" );
	if ( !parser.success( ) )
		return -1;

	auto a = parser.get_subkey( R"(ControlSet001)", R"(ControlSet001/Services/BITS)" );
	for ( const auto& keys : a.keys_list(  ) )
		std::cout << keys << std::endl;

	for ( const auto& sub_keys : a.subkeys_list(  ) )
		std::cout << sub_keys << std::endl;

	std::cout << std::endl << std::endl;

	std::cout << "DelayedAutostart: " << a.get_key_value<int>( "DelayedAutostart" ) << std::endl;
	std::cout << "DisplayName: " << a.get_key_value<std::string>( "DisplayName" ) << std::endl;
	std::cout << "ImagePath: " << a.get_key_value<std::string>( "ImagePath" ) << std::endl;

	std::cout << "RequiredPrivileges: ";
	for ( const auto& val : a.get_key_value<std::vector<std::string>>( "RequiredPrivileges" ) )
		std::cout << val << ", ";

	std::cout << std::endl;
	return 0;
}
```
