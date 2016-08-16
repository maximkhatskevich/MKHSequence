# https://github.com/jcampbell05/xcake
# http://www.rubydoc.info/github/jcampbell05/xcake/master/file/docs/Cakefile.md

project.name = "MKHSequence"
project.class_prefix = "SEQ"
project.organization = "Maxim Khatskevich"

#===

project.all_configurations.each do |configuration|

    configuration.settings["SDKROOT"] = "iphoneos"
    configuration.settings["DEBUG_INFORMATION_FORMAT"] = "dwarf"
    configuration.settings["CODE_SIGN_IDENTITY[sdk=iphoneos*]"] = "iPhone Developer"
    configuration.settings["TARGETED_DEVICE_FAMILY"] = "1,2"
    configuration.settings["IPHONEOS_DEPLOYMENT_TARGET"] = 8.4
    configuration.settings["VERSIONING_SYSTEM"] = "apple-generic"

    configuration.settings["GCC_NO_COMMON_BLOCKS"] = "YES"
    configuration.settings["GCC_WARN_ABOUT_RETURN_TYPE"] = "YES_ERROR"
    configuration.settings["GCC_WARN_UNINITIALIZED_AUTOS"] = "YES_AGGRESSIVE"
    configuration.settings["CLANG_WARN_DIRECT_OBJC_ISA_USAGE"] = "YES_ERROR"
    configuration.settings["CLANG_WARN_OBJC_ROOT_CLASS"] = "YES_ERROR"

    configuration.settings["SWIFT_OPTIMIZATION_LEVEL"] = "-Onone"

    configuration.settings["CURRENT_PROJECT_VERSION"] = "1" # just default non-empty value

    #===

    if configuration.name == "Release"

        configuration.settings["DEBUG_INFORMATION_FORMAT"] = "dwarf-with-dsym"

    end

end

#=== Targets

target do |target|

    target.name = project.name
    target.type = :framework
    target.language = :swift
    target.platform = :ios
    target.deployment_target = 8.0

    target.all_configurations.each do |configuration|

        #=== Build Settings - Core

        configuration.product_bundle_identifier = "khatskevich.maxim." + target.name

        configuration.settings["INFOPLIST_FILE"] = "Info/" + target.name + ".plist"

        configuration.settings["PRODUCT_NAME"] = "$(TARGET_NAME)"

        # This will show "Automatic" in Xcode,
        # relies on proper/valid "PROVISIONING_PROFILE" value:
        configuration.settings["CODE_SIGN_IDENTITY[sdk=iphoneos*]"] = nil

    end

    #=== Source Files

    target.include_files = ["Src/**/*.*"]
    target.include_files << "Src-Extra/**/*.*"

    #=== Tests
    
    unit_tests_for target do |test_target|
        
        test_target.name = target.name + "Tst"

        test_target.all_configurations.each do |configuration|

            configuration.product_bundle_identifier = "khatskevich.maxim." + test_target.name

            configuration.settings["INFOPLIST_FILE"] = "Info/" + test_target.name + ".plist"

            configuration.settings["LD_RUNPATH_SEARCH_PATHS"] = "$(inherited) @executable_path/Frameworks @loader_path/Frameworks"

        end

        #=== Source Files

        test_target.include_files = ["Tst/**/*.*"]

    end

end