==================
standalone backend
==================

Overview
~~~~~~~~

In standalone backend, all certificates, keys and CSRs are stored locally on
ansible controller as files.
It uses community.crypto collection to generate CSR, sign certificates etc.

Prerequisites
~~~~~~~~~~~~~

None. This role can prepare everything from scratch on ansible controller.

Limitations
~~~~~~~~~~~

- private keys cannot be stored in encrypted form on ansible controller.
  It's due to the fact that this backend uses community.crypto modules
  without "_pipe" suffix, which means it reads/writes directly from/to files
  without a possibility to decrypt/encrypt them "in a fly".

Additional Information
~~~~~~~~~~~~~~~~~~~~~~

- Certificate keys are stored in `pki_dir` on ansible controller.
  It is a common practice for this folder to be part of the git repository.
  If that's the case, please consider encrypting keys before storing them in
  git repository(but see "Limitations" section first, because in most cases
  it's needed to decrypt all keys on ansible controller before running
  playbooks).

Variables
~~~~~~~~~

pki_authorities
---------------

.. list-table::
   :header-rows: 1
   :widths: 20 1 79
   :align: left

   * - Variable
     - Required
     - Description
   * - backend
     - 𐄂
     - PKI backend that should be used for this certificate.
   * - backup
     - 𐄂
     - Create a backup file including a timestamp so you can get the original private key back if you overwrote it with a new one by accident.
   * - basic_constraints
     - 𐄂
     - Indicates basic constraints, such as if the certificate is a CA.
   * - cn
     - 𐄂
     - Common name of a certificate.
   * - country_name
     - 𐄂
     - Specifies the C (Country) values in the subject field of the resulting certificate.
   * - key_group
     - 𐄂
     - Name of the group that should own the filesystem object, as would be fed to chown.
   * - key_mode
     - 𐄂
     - The permissions the resulting filesystem object should have.
   * - key_owner
     - 𐄂
     - Name of the user that should own the filesystem object, as would be fed to chown.
   * - key_passphrase
     - 𐄂
     - The passphrase for the private key.
   * - key_usage
     - 𐄂
     - This defines the purpose (for example encipherment, signature, certificate signing) of the key contained in the certificate.
   * - locality_name
     - 𐄂
     - Specifies the L (Locality) values in the subject field of the resulting certificate.
   * - name
     - ✔
     - Name of the certificate (used mainly to find the right authority when installing it on target hosts).
   * - not_after
     - 𐄂
     - Set the Not After field of the certificate with specified date value.
   * - organization_name
     - 𐄂
     - Specifies the O (Organization) values in the subject field of the resulting certificate.
   * - organization_unit_name
     - 𐄂
     - Specifies the OU (OrganizationalUnit) values in the subject field of the resulting certificate.
   * - provider
     - ✔
     - Name of the provider to use to generate/retrieve the OpenSSL certificate.
   * - signed_by
     - 𐄂
     - The issuer name of this certificate.
   * - state_or_province_name
     - 𐄂
     - Specifies the ST (Province) values in the subject field of the resulting certificate.
   * - subject
     - 𐄂
     - Key/value pairs that will be present in the subject name field of the certificate signing request.
   * - ttl
     - 𐄂
     - Specifies the requested Time To Live (after which the certificate will be expired).


pki_install_ca
--------------

.. list-table::
   :header-rows: 1
   :widths: 20 1 79
   :align: left

   * - Variable
     - Required
     - Description
   * - filename
     - 𐄂
     - Name for the file containing the authority on the target hosts
   * - name
     - ✔
     - Name of the authority to install
   * - src
     - 𐄂
     - Name for the source file containing the authority on the ansible controller

pki_certificates
----------------

.. list-table::
   :header-rows: 1
   :widths: 20 1 79
   :align: left

   * - Variable
     - Required
     - Description
   * - backend
     - 𐄂
     - PKI backend that should be used for this certificate.
   * - basic_constraints
     - 𐄂
     - Indicates basic constraints, such as if the certificate is a CA.
   * - cn
     - ✔
     - Common name of a certificate.
   * - country_name
     - 𐄂
     - Specifies the C (Country) values in the subject field of the resulting certificate.
   * - extended_key_usage
     - 𐄂
     - Additional restrictions (for example client authentication, server authentication) on the allowed purposes for which the public key may be used.
   * - key_format
     - 𐄂
     - Specifies the private key format.
   * - key_passphrase
     - 𐄂
     - The passphrase for the private key.
   * - key_usage
     - 𐄂
     - This defines the purpose (for example encipherment, signature, certificate signing) of the key contained in the certificate.
   * - locality_name
     - 𐄂
     - Specifies the L (Locality) values in the subject field of the resulting certificate.
   * - name
     - ✔
     - Name of the certificate (used mainly to find the right certificate when installing it on target hosts).
   * - organization_name
     - 𐄂
     - Specifies the O (Organization) values in the subject field of the resulting certificate.
   * - organization_unit_name
     - 𐄂
     - Specifies the OU (OrganizationalUnit) values in the subject field of the resulting certificate.
   * - provider
     - 𐄂
     - Name of the provider to use to generate/retrieve the OpenSSL certificate.
   * - san
     - 𐄂
     - A dictionary containing dns, ip, uri and other SANs.
   * - signed_by
     - ✔
     - The issuer name of this certificate.
   * - state_or_province_name
     - 𐄂
     - Specifies the ST (Province) values in the subject field of the resulting certificate.
   * - subject
     - 𐄂
     - Key/value pairs that will be present in the subject name field of the certificate signing request.
   * - ttl
     - 𐄂
     - Specifies the requested Time To Live (after which the certificate will be expired).

pki_install_certificates
------------------------

.. list-table::
   :header-rows: 1
   :widths: 20 1 79
   :align: left

   * - Variable
     - Required
     - Description
   * - dest
     - ✔
     - Path where certificate should be stored on a target host.
   * - group
     - 𐄂
     - Name of the group that should own the filesystem object, as would be fed to chown.
   * - mode
     - 𐄂
     - The permissions the resulting filesystem object should have.
   * - owner
     - 𐄂
     - Name of the user that should own the filesystem object, as would be fed to chown.
   * - name
     - 𐄂
     - Name of the certificate that should be installed on a target host. Either 'name' or 'src' is required.
   * - src
     - 𐄂
     - Path where source certificate is stored on ansible controller. Either 'name'  or 'src' is required. 'src' should be used primarly for user-defined certificates that reside in custom paths.
   * - type
     - 𐄂
     - Required when 'name' is set. Specifies the content that should be placed in a destination file. Accepted values: certificate, certificate_chain, ca_bundle, private_key.
