## Emacs config

Copy the following into a .emacs file in `~/` directory

```
(require 'package)
(let* ((no-ssl (and (memq system-type '(windows-nt ms-dos))
                    (not (gnutls-available-p))))
       (proto (if no-ssl "http" "https")))
  (when no-ssl (warn "\
Your version of Emacs does not support SSL connections,
which is unsafe because it allows man-in-the-middle attacks.
There are two things you can do about this warning:
1. Install an Emacs version that does support SSL and be safe.
2. Remove this warning from your init file so you won't see it again."))
  (add-to-list 'package-archives (cons "melpa" (concat proto "://melpa.org/packages/")) t)
  ;; Comment/uncomment this line to enable MELPA Stable if desired.  See `package-archive-priorities`
  ;; and `package-pinned-packages`. Most users will not need or want to do this.
  ;;(add-to-list 'package-archives (cons "melpa-stable" (concat proto "://stable.melpa.org/packages/")) t)
  )
(package-initialize)


(add-to-list 'package-archives
             '("melpa-stable" . "https://stable.melpa.org/packages/") t)
(custom-set-variables
 ;; custom-set-variables was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(custom-enabled-themes (quote (dracula)))
 '(custom-safe-themes
   (quote
    ("55c2069e99ea18e4751bd5331b245a2752a808e91e09ccec16eb25dadbe06354" default)))
 '(inhibit-startup-screen t)
 '(package-selected-packages
   (quote
    (markdown-mode+ md-readme auto-complete-clang-async company-ycmd auto-complete-clang auto-complete modern-cpp-font-lock clang-format company-irony-c-headers company-irony company dracula-theme neotree))))
(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 )

(add-hook 'after-init-hook 'global-company-mode)

(global-set-key [f5] 'linum-mode)


(require 'neotree)
(global-set-key [f8] 'neotree-toggle)

(global-set-key [f6] 'other-frame)
(global-set-key [f7] 'make-frame-command)
(global-set-key [f12] 'delete-frame)

(show-paren-mode 1)




; clang-format can be triggered using C-c C-f
;; Create clang-format file using google style
;; clang-format -style=google -dump-config > .clang-format
(require 'clang-format)
(global-set-key (kbd "C-c C-f") 'clang-format-region)


(require 'modern-cpp-font-lock)
(modern-c++-font-lock-global-mode t)

(add-hook 'after-init-hook 'global-company-mode)

```
